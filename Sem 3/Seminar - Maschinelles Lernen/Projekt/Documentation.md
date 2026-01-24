
# Training
## 1. Training
- Erstes Traing startet - robot "stirbt" die ganze Zeit aufgrund von ee_body_pos
- Fast 100% aller Episoden enden durch Error im Endeffctor/body Pos
- Goal sollte eig seinist eigentlich episode Time out

- Anpassung Parameter in `booster_train\source\booster_train\booster_train\tasks\manager_based\beyond_mimic\robots\k1\fight_001\tracking_env_cfg.py`  -> 

  ```python
  ee_body_pos = DoneTerm(
        func=mdp.bad_motion_body_pos_z_only,
        params={
            "command_name": "motion",
            "threshold": 0.25 -> 0.75,
            "body_names": [
                "left_hand_link",
                "right_hand_link",
                "left_foot_link",
                "right_foot_link",
            ],
        },
  ```

Termination gelocket. Nicht mehr so streng mit der Body position sein. Denn davor

>Die Endeffector-Positionsabweichung ist in fast allen Fällen **> 25 cm** → Episode wird sofort gekillt.

## 2. Training

- Termination durch `ee_body_pos` in früher Phase deutlich gesunken von 0,99 -> 0,09 - 0,2
- In früher Phase noch keine Termination durch `time_out`. 
	- Größter Terminator in dieser Phase mit bis zu 99% `anchor_pos`
- Durchschnittliche Episodenlänge nach 9,4Mio Timesteps: 60-70
- `time_out` bleibt auch nach 12Mio steps bei 0%

Vorzeitg beendet nach 13Mio steps da nie `time_out` Episode

## 3. Training

Starting with:

```powershell
python.bat C:\Users\<USER>\rl_walk\booster_train\scripts\rsl_rl\train.py --task=Booster-K1-Fight_001-v0 --headless --device cuda:0```
```

  ```python
  ee_body_pos = DoneTerm(
        func=mdp.bad_motion_body_pos_z_only,
        params={
            "command_name": "motion",
            "threshold": 0.5, #changed threshold from 0.25 to 0.5
            "body_names": [
                "left_hand_link",
                "right_hand_link",
                "left_foot_link",
                "right_foot_link",
            ],
        },
  ```
- Nach 1400 Iterationen steigt `time_out` deutlich -> 60% training geht also voran
- Mean episode length: 374.31
![[Pasted image 20260124141509.png]]

- das momentan ab vielversprechendste Training
- GPU stats während des Trainings:
 ![[Pasted image 20260124151621.png]]

# Play

![[Pasted image 20260124161335.png]]

Play in Isaac Sim