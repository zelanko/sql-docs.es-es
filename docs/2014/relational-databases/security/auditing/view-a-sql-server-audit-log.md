---
title: Ver un registro de SQL Server Audit | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8f9902a4fc92ef0b35bae62eb80170762c52fdec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055448"
---
# <a name="view-a-sql-server-audit-log"></a>Ver un registro de SQL Server Audit
  Este tema describe cómo ver un registro de auditoría de SQL Server en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver un registro de auditoría de SQL Server, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso `CONTROL SERVER`.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Para ver un registro de auditoría de SQL Server  
  
1.  En el Explorador de objetos, expanda la carpeta **Seguridad** .  
  
2.  Expanda la carpeta **Auditorías** .  
  
3.  Haga clic con el botón derecho en el registro de auditoría que quiera ver y seleccione **Ver registros de auditoría**. Se abrirá el cuadro **de diálogo Visor del archivo de registros-**_SERVER_NAME_ . Para más información, consulte [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md).  
  
4.  Cuando termine, haga clic en **Cerrar**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] le recomienda ver el registro de auditoría mediante el Visor del archivo de registros. Pero, si está creando un sistema de supervisión automatizado, puede leer la información en el archivo de auditoría directamente si usa la función [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql). Si lee el archivo directamente, los datos tendrán un formato ligeramente diferente (sin procesar). Consulte **sys.fn_get_audit_file** para obtener más información  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Audit &#40;motor de base de datos&#41;](sql-server-audit-database-engine.md)   
 [Escribir eventos de SQL Server Audit en el registro de seguridad](write-sql-server-audit-events-to-the-security-log.md)  
  
  
