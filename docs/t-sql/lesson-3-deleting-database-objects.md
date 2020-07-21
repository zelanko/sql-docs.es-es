---
title: 'Tutorial de T-SQL: Eliminación de objetos de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 07/30/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: ecf26dd5-4535-4ed6-86fc-c73f9d9dedec
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 36b68bb833c5c95beeb65b792b9621f2f9bb9c4f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68031572"
---
# <a name="lesson-3-delete-database-objects"></a>Lección 3: Eliminar objetos de base de datos
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Esta breve lección quita los objetos que ha creado en las lecciones 1 y 2 y, a continuación, quita la base de datos.  
  
Antes de eliminar objetos, asegúrese de que está en la base de datos correcta:
  
  ```sql  
  USE TestData;  
  GO  
  ```  

## <a name="revoke-stored-procedure-permissions"></a>Revocación permisos de procedimientos almacenados
  
Use la instrucción `REVOKE` para quitar el permiso de ejecución para `Mary` en el procedimiento almacenado:
  
  ```sql  
  REVOKE EXECUTE ON pr_Names FROM Mary;  
  GO  
  ```  
  
## <a name="drop-permissions"></a>Rescisión de permisos

1. Use la instrucción `DROP` para quitar el permiso de `Mary` para tener acceso a la base de datos `TestData` :
  
   ```sql  
   DROP USER Mary;  
   GO  
   ```  


2. Use la instrucción `DROP` para quitar el permiso de `Mary` para tener acceso a esta instancia de [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]:
  
   ```sql  
   DROP LOGIN [<computer_name>\Mary];  
   GO   
   ```  
  
3. Use la instrucción `DROP` para quitar el procedimiento almacenado `pr_Names`:  
  
   ```sql  
   DROP PROC pr_Names;  
   GO   
   ```  
  
4. Use la instrucción `DROP` para quitar la vista `vw_Names`:  
  
   ```sql  
   DROP VIEW vw_Names;  
   GO  
   ```  

## <a name="delete-table"></a>Eliminación de tablas
  
1. Use la instrucción `DELETE` para quitar todas las filas de la tabla `Products` :  
  
    ```sql  
    DELETE FROM Products;  
    GO  
    ```  
  
2.  Use la instrucción `DROP` para quitar la tabla `Products` :  
  
    ```sql  
    DROP TABLE Products;  
    GO    
    ```  

## <a name="remove-database"></a>Eliminación de bases de datos
  
No puede quitar la base de datos `TestData` mientras esté en la base de datos; por tanto, cambie primero el contexto a otra base de datos y, a continuación, use la instrucción `DROP` para quitar la base de datos `TestData` :  
  
  ```sql  
  USE MASTER;  
  GO  
  DROP DATABASE TestData;  
  GO   
  ```  
  
Esto finaliza el tutorial de escritura de instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] . Recuerde que este tutorial es una introducción breve y en él no se describen todas las opciones de las instrucciones que se usan. El diseño y la creación de una estructura de base de datos eficaz y la configuración del acceso seguro a los datos requiere una base de datos más compleja que la que se muestra en este tutorial.  

  
  
