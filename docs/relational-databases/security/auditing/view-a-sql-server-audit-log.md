---
title: Ver un registro de SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: security
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0d40461b7f97456493017852adc7749fd78c4911
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033748"
---
# <a name="view-a-sql-server-audit-log"></a>Ver un registro de SQL Server Audit
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tema describe cómo ver un registro de auditoría de SQL Server en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver un registro de auditoría de SQL Server, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso **CONTROL SERVER** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Para ver un registro de auditoría de SQL Server  
  
1.  En el Explorador de objetos, expanda la carpeta **Seguridad** .  
  
2.  Expanda la carpeta **Auditorías** .  
  
3.  Haga clic con el botón derecho en el registro de auditoría que quiera ver y seleccione **Ver registros de auditoría**. Así, se abre el cuadro de diálogo **Visor del archivo de registros –***nombre_servidor*. Para más información, consulte [Log File Viewer F1 Help](../../../relational-databases/logs/log-file-viewer-f1-help.md).  
  
4.  Cuando termine, haga clic en **Cerrar**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] le recomienda ver el registro de auditoría mediante el Visor del archivo de registros. Pero, si está creando un sistema de supervisión automatizado, puede leer la información en el archivo de auditoría directamente si usa la función [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). Si lee el archivo directamente, los datos tendrán un formato ligeramente diferente (sin procesar). Vea **sys.fn_get_audit_file** para obtener más información.  
  
## <a name="see-also"></a>Ver también  
 [SQL Server Audit &#40;motor de base de datos&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md)   
 [Escribir eventos de auditoría de SQL Server en el registro de seguridad](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
  
