---
title: Iniciar o detener un conjunto de recopilación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- collection sets [SQL Server], stopping
- collection sets [SQL Server], starting
ms.assetid: 48a7b2fe-6bc3-4278-a7ec-1babc1290345
caps.latest.revision: 19
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dc02f46c94fb4297428ee2a410a79626d516ae85
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199371"
---
# <a name="start-or-stop-a-collection-set"></a>Iniciar o detener un conjunto de recopilación
  En este tema se describe cómo iniciar o detener un conjunto de recopilación en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para iniciar o detener un conjunto de recopilación, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los procedimientos almacenados y las vistas de catálogo del recopilador de datos se almacenan en la base de datos **msdb** .  
  
-   A diferencia de los procedimientos almacenados normales, los parámetros de los procedimientos del  recopilador de datos deben escribirse de forma precisa y no admiten la conversión automática de tipos de datos. Si no se llama a estos parámetros con los tipos de datos de parámetros de entrada correctos, según se especifica en la descripción del argumento, el procedimiento almacenado devuelve un error.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Debe iniciarse el Agente SQL Server.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Para obtener información sobre los conjuntos de recopilación, consulte la vista de catálogo [syscollector_collection_sets](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql) .  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere la pertenencia al rol fijo de base de datos **dc_operator** . Si el conjunto de recopilación no tiene una cuenta de proxy, es necesaria la pertenencia al rol fijo de servidor **sysadmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-start-a-collection-set"></a>Para iniciar un conjunto de recopilación  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** , expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.  
  
2.  Haga clic con el botón derecho en el conjunto de recopilación que quiere iniciar y, luego, haga clic en **Iniciar conjunto de recopilación de datos**.  
  
     Un cuadro de mensaje muestra los resultados de esta acción y una flecha verde en el icono para el conjunto de recopilación indica que el conjunto de recopilación se ha iniciado.  
  
#### <a name="to-stop-a-collection-set"></a>Para detener un conjunto de recopilación  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** , expanda **Recopilación de datos**y, después, **Conjuntos de recopilación de datos del sistema**.  
  
2.  Haga clic con el botón derecho en el conjunto de recopilación que quiere detener y, luego, haga clic en **Detener conjunto de recopilación de datos**.  
  
     Un cuadro de mensaje muestra los resultados de esta acción y un círculo rojo en el icono para el conjunto de recopilación indica que el conjunto de recopilación se ha detenido.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-start-a-collection-set"></a>Para iniciar un conjunto de recopilación  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usa [sp_syscollector_start_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql) para iniciar el conjunto de recopilación cuyo identificador es `1`.  
  
```tsql  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
#### <a name="to-stop-a-collection-set"></a>Para detener un conjunto de recopilación  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usa [sp_syscollector_stop_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql) para detener el conjunto de recopilación cuyo identificador es `1`.  
  
```tsql  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Vistas del recopilador de datos &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/data-collector-views-transact-sql)   
 [Recopilación de datos](data-collection.md)  
  
  
