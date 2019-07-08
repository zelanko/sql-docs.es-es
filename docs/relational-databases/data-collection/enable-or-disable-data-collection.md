---
title: Habilitar o deshabilitar la recopilación de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], disabling
- data collector [SQL Server], enabling
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0579405abb9a8b84d56e94db88a1a2a77f1d99d1
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67586010"
---
# <a name="enable-or-disable-data-collection"></a>Habilitar o deshabilitar la recopilación de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo habilitar o deshabilitar una recopilación de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para habilitar o deshabilitar una recopilación de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere la pertenencia al rol fijo de base de datos **dc_admin** o **dc_operator** (con permiso EXECUTE) para ejecutar este procedimiento.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-enable-the-data-collector"></a>Para habilitar el recopilador de datos  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** .  
  
2.  Haga clic con el botón derecho en **Recopilación de datos**y luego haga clic en **Habilitar recopilación de datos**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

#### <a name="to-disable-the-data-collector"></a>Para deshabilitar el recopilador de datos  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** .  
  
2.  Haga clic con el botón derecho en **Recopilación de datos**y luego haga clic en **Deshabilitar recopilación de datos**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-enable-the-data-collector"></a>Para habilitar el recopilador de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usa [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) para habilitar el recopilador de datos.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### <a name="to-disable-the-data-collector"></a>Para deshabilitar el recopilador de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usa [sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md) para deshabilitar el recopilador de datos.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
