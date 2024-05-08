# cpu-npu-ram-
//


# 고성능 전원 모드 설정
powercfg -setactive SCHEME_MIN

# 시각 효과 최소화
SystemPropertiesPerformance.exe /pagefile

# 디스크 정리
cleanmgr /sagerun:1

# 백그라운드 앱 비활성화 (사용자의 선택에 따라 실행해야 함)
Get-AppxPackage | Where-Object { $_.NonRemovable -eq $false } | Remove-AppxPackage


가상의 npu 프로세스 탑재 스크립트
# 가상 NPU 프로세스 탑재 스크립트 예시
def load_virtual_npu_process():
    # 가상 NPU 프로세스를 초기화하고 설정합니다.
    npu_config = {
        'model_path': '/path/to/your/model.onnx',
        'memory_limit': 4096,  # 메모리 제한 설정 (MB 단위)
        'num_threads': 4,      # 병렬 처리 스레드 수
        'power_mode': 'high',  # 전력 모드 설정 (high, balanced, low)
    }

    # 가상 NPU 프로세스를 시작합니다.
    npu_process = VirtualNPUProcess(npu_config)
    npu_process.start()

    # 모델 로드 및 추론 예시
    model = load_model(npu_config['model_path'])
    input_data = prepare_input_data()  # 입력 데이터 준비
    output = model.infer(input_data)   # 모델 추론

    # 가상 NPU 프로세스 종료
    npu_process.stop()

if __name__ == '__main__':
    load_virtual_npu_process()


