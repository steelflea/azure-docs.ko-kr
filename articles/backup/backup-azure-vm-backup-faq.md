---
title: Azure VM 백업 FAQ
description: Azure VM 백업 작동 방식, 제한 및 정책 변경 시 발생하는 상황과 관련된 일반적인 질문에 대한 대답입니다.
services: backup
author: trinadhk
manager: shreeshd
keywords: Azure VM 백업, Azure VM 복원, 백업 정책
ms.service: backup
ms.topic: conceptual
ms.date: 8/16/2018
ms.author: trinadhk
ms.openlocfilehash: ff97d164ee8b2059e1b46377067041d6c381052b
ms.sourcegitcommit: 3dcb1a3993e51963954194ba2a5e42260d0be258
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50753970"
---
# <a name="questions-about-the-azure-vm-backup-service"></a>Azure VM Backup 서비스에 대한 질문
이 문서에서는 Azure VM Backup 구성 요소를 빨리 이해하는 데 도움이 되는 일반적인 질문에 대한 대답을 제공합니다. 대답 중 일부에는 포괄적인 정보를 포함하는 문서에 대한 링크가 있습니다. 또한 [토론 포럼](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazureonlinebackup)에 Azure Backup 서비스에 대한 질문도 게시할 수 있습니다.

## <a name="configure-backup"></a>백업 구성
### <a name="do-recovery-services-vaults-support-classic-vms-or-resource-manager-based-vms-br"></a>Recovery Services 자격 증명 모음은 클래식 VM 또는 Resource Manager 기반 VM을 지원하나요? <br/>
Recovery Services 자격 증명 모음은 두 모델을 모두 지원합니다.  클래식 VM 또는 Resource Manager VM을 Recovery Services 자격 증명 모음에 백업할 수 있습니다.

### <a name="what-configurations-are-not-supported-by-azure-vm-backup"></a>Azure VM 백업에서 지원되지 않는 구성은 무엇인가요?
[지원되는 운영 체제](backup-azure-arm-vms-prepare.md#supported-operating-systems-for-backup) 및 [VM 백업 제한](backup-azure-arm-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)을 참조하세요.

### <a name="why-cant-i-see-my-vm-in-configure-backup-wizard"></a>백업 구성 마법사에서 내 VM을 볼 수 없는 이유는 무엇인가요?
백업 구성 마법사에서 Azure Backup은 다음과 같은 VM만 나열합니다.
  * 아직 보호되지 않음 - VM 블레이드로 이동하고 설정 메뉴에서 Backup 상태를 확인하여 VM의 백업 상태를 확인할 수 있습니다. [VM의 백업 상태를 확인하는 방법](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-vm-operations-menu)에 대해 자세히 알아보세요.
  * VM과 동일한 지역에 속함

## <a name="backup"></a>Backup
### <a name="will-on-demand-backup-job-follow-same-retention-schedule-as-scheduled-backups"></a>주문형 백업 작업은 예약된 백업과 동일한 보존 일정을 따르나요?
아니요. 주문형 백업 작업의 보존 범위를 지정해야 합니다. 기본적으로 포털에서 트리거된 이후 30일 동안 유지됩니다.

### <a name="i-recently-enabled-azure-disk-encryption-on-some-vms-will-my-backups-continue-to-work"></a>최근에 일부 VM에서 Azure Disk Encryption을 사용할 수 있습니다. 내 백업이 계속 작동하나요?
Key Vault에 액세스하려면 Azure Backup 서비스에 대한 권한을 부여해야 합니다. [PowerShell 설명서](backup-azure-vms-automation.md)의 *Backup 사용* 섹션에서 설명하는 단계를 사용하여 PowerShell에서 이러한 권한을 제공할 수 있습니다.

### <a name="i-migrated-disks-of-a-vm-to-managed-disks-will-my-backups-continue-to-work"></a>VM 디스크를 관리 디스크로 마이그레이션했습니다. 내 백업이 계속 작동하나요?
예, 백업이 원활하게 작동하므로 백업을 다시 구성할 필요가 없습니다.

### <a name="my-vm-is-shut-down-will-an-on-demand-or-a-scheduled-backup-work"></a>내 VM이 종료되었습니다. 요청 시 또는 예약된 백업 작업도 종료되나요?
예. 컴퓨터가 종료되어도 백업 작업 및 복구 지점은 충돌 일치로 표시됩니다. 자세한 내용은 [이 문서](backup-azure-vms-introduction.md#how-does-azure-back-up-virtual-machines)의 데이터 일관성 섹션을 참조하세요.

### <a name="can-i-cancel-an-in-progress-backup-job"></a>진행 중인 백업 작업을 취소할 수 있나요?
예. "스냅숏 만들기" 단계에 있는 경우 백업 작업을 취소할 수 있습니다. **스냅숏에서 데이터 전송이 진행 중인 경우 작업을 취소할 수 없습니다**.

### <a name="i-enabled-resource-group-lock-on-my-backed-up-managed-disk-vms-will-my-backups-continue-to-work"></a>백업한 관리 디스크 VM에서 리소스 그룹 잠금을 사용하도록 설정했습니다. 내 백업이 계속 작동하나요?
사용자가 리소스 그룹을 잠그는 경우 Backup 서비스는 이전 복원 지점을 삭제할 수 없습니다. 이로 인해, 백 엔드에서 적용된 최대 18개의 복원 지점 제한에 도달했으므로 새 백업이 시작되지 못합니다. RG 잠금 후에 내부 오류로 인해 백업이 실패하는 경우 다음 [단계에 따라 복원 지점 컬렉션을 제거](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md#clean-up-restore-point-collection-from-azure-portal)합니다.

### <a name="does-backup-policy-take-daylight-saving-timedst-into-account"></a>Backup 정책에서 DST(일광 절약 시간)을 고려합니까?
아니요. 로컬 컴퓨터의 날짜 및 시간은 현재 일광 절약 시간을 보정하여 현지 시간으로 표시됩니다. 따라서 예약된 백업에 대해 구성된 시간이 DST 때문에 현지 시간과 다를 수 있습니다.

### <a name="maximum-of-how-many-data-disks-can-i-attach-to-a-vm-to-be-backed-up-by-azure-backup"></a>Azure Backup을 통해 백업할 VM에는 데이터 디스크를 몇 개까지 연결할 수 있나요?
Azure Backup은 현재 최대 16개 디스크가 포함된 가상 머신 백업을 지원합니다. 16개 디스크를 모두 지원하려면 [Azure VM Backup 스택 V2로 업그레이드](backup-upgrade-to-vm-backup-stack-v2.md)하세요. 2018년 9월 24일부터는 보호 가능한 모든 VM이 지원될 예정입니다.

### <a name="does-azure-backup-support-standard-ssd-managed-disk"></a>Azure Backup은 표준 SSD Managed Disks를 지원하나요?
Azure Backup은 Microsoft Azure Virtual Machines용의 새로운 지속형 저장소 유형인 [표준 SSD Managed Disks](https://azure.microsoft.com/blog/announcing-general-availability-of-standard-ssd-disks-for-azure-virtual-machine-workloads/)를 지원합니다. 이 저장소는 [Azure VM Backup 스택 V2](backup-upgrade-to-vm-backup-stack-v2.md)의 Managed Disks에서 지원됩니다.

## <a name="restore"></a>복원
### <a name="how-do-i-decide-between-restoring-disks-versus-full-vm-restore"></a>디스크 복원과 전체 VM 복원 중에서 어떻게 결정해야 하나요?
Azure 전체 VM 복원을 빠른 만들기 옵션으로 생각해 볼 수 있습니다. VM 복원 옵션은 디스크의 이름, 해당 디스크에서 사용되는 컨테이너, 공용 IP 주소 및 네트워크 인터페이스 이름을 변경합니다. 이러한 변경은 VM 생성 동안 만들어진 리소스의 고유성을 유지하는 데 필요합니다. 하지만 가용성 집합에 VM이 추가되지는 않습니다.

복원 디스크를 사용하여 다음을 수행합니다.
  * 크기를 변경하는 것처럼 특정 시점의 구성에서 만든 VM을 사용자 지정합니다.
  * 백업 시 존재하지 않는 구성을 추가합니다.
  * 만드는 리소스에 대한 명명 규칙을 제어합니다.
  * 가용성 집합에 VM을 추가합니다.
  * PowerShell/선언적 템플릿 정의를 통해서만 설정할 수 있는 기타 구성

### <a name="can-i-use-backups-of-unmanaged-disk-vm-to-restore-after-i-upgrade-my-disks-to-managed-disks"></a>내 디스크를 관리 디스크로 업그레이드한 후 관리되지 않는 디스크 VM의 백업을 사용하여 복원할 수 있나요?
예, 관리되지 않는 디스크에서 관리 디스크로 마이그레이션하기 전에 수행한 백업을 사용할 수 있습니다. 기본적으로 VM 복원 작업은 관리되지 않는 디스크가 있는 VM을 만듭니다. 디스크 복원 기능을 사용하여 디스크를 복원하고 이를 사용하여 관리 디스크에 VM을 만들 수 있습니다.

### <a name="what-is-the-procedure-to-restore-a-vm-to-a-restore-point-taken-before-the-conversion-from-unmanaged-to-managed-disks-was-done-for-a-vm"></a>VM에 대해 관리되지 않는 디스크에서 관리 디스크로 변환하기 전에 선택한 복원 지점으로 VM을 복원하는 절차는 무엇인가요?
이 시나리오에서는 기본적으로 VM 복원 작업을 통해 관리되지 않는 디스크가 있는 VM을 만듭니다. 관리 디스크가 있는 VM을 만들려면 다음을 수행합니다.
1. [관리되지 않는 디스크에 복원](tutorial-restore-disk.md#restore-a-vm-disk)
2. [복원된 디스크를 관리 디스크로 변환](tutorial-restore-disk.md#convert-the-restored-disk-to-a-managed-disk)
3. [관리 디스크가 있는 VM 만들기](tutorial-restore-disk.md#create-a-vm-from-the-restored-disk) <br>
PowerShell cmdlet의 경우 [여기](backup-azure-vms-automation.md#restore-an-azure-vm)를 참조하세요.

### <a name="can-i-restore-the-vm-if-my-vm-is-deleted"></a>삭제된 VM을 복원할 수 있나요?
예. VM의 수명 주기와 해당 백업 항목은 서로 다릅니다. 따라서 VM을 삭제하더라도 Recovery Services 자격 증명 모음에서 해당 항목으로 이동한 후 복구 지점 중 하나를 사용하여 복원을 트리거할 수 있습니다.

## <a name="manage-vm-backups"></a>VM 백업 관리
### <a name="what-happens-when-i-change-a-backup-policy-on-vms"></a>VM에서 백업 정책을 변경하면 어떻게 되나요?
VM에 새 정책을 적용하면 새 정책의 일정 및 보존이 수행됩니다. 보존 기간을 늘리면 기존 복구 지점이 새 정책에 따라 유지되도록 표시됩니다. 보존 기간을 줄이면 다음 정리 작업에서 정리(prune) 표시되고 결과적으로 삭제됩니다.

### <a name="how-can-i-move-a-vm-enrolled-in-azure-backup-between-resource-groups"></a>Azure Backup에 등록된 VM을 리소스 그룹 간에 이동할 수 있습니까?
아래 단계를 따라 백업된 VM을 대상 리소스 그룹으로 이동합니다.
1. 일시적으로 백업을 중단하고 백업 데이터를 보존
2. VM을 대상 리소스 그룹으로 이동
3. 동일/새 자격 증명 모음으로 다시 보호

사용자는 이동 작업 전에 만든 사용 가능한 복원 지점으로부터 복원할 수 있습니다.
