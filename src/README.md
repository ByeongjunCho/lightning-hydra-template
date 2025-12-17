# 수정내역
## wandb sweep
- lightning hydra template 에 wandb sweep를 실행할 수 있도록 수정
- sweep 실행을 위한 `.yaml` 작성 : wandb documents 참고
- `sweep.yaml` 예시 참고

<br>

```
# sweep.yaml
program: train.py
method: bayes
metric:
goal: maximize
name: val/acc_best
parameters:
model.optimizer.lr:
    min: 0.0001
    max: 0.01
data.batch_size:
    values: [2048]
trainer:
    values: [ddp]
trainer.max_epochs:
    values: [3]

command:
- ${env}
- python
- ${program}
- ${args_no_hyphens}

```
### 실행
1. ` wandb sweep --project sweep-demo-cli sweep.yaml` 
    - 명령어 실행 시 wnadb id 가 발급됨
2. `wandb agent --count 5 byeongjuncho/sweep-demo-cli/{발급된 sweep id}`
    - 발급된 id 를 사용하여 sweep 실행
    - count를 설정하여 최대 실행 개수를 조정할 수 있음

### 기타 wandb 관련
[링크](https://api.wandb.ai/links/wandb/per7natm)