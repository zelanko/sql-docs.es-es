---
title: Creación de una clave maestra de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
ms.reviewer: carlrab
ms.openlocfilehash: cb8305d9d5a3c72e6dffafd231f21110a5abdd14
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055343"
---
# <a name="create-a-database-master-key"></a>Crear la clave maestra de una base de datos

En este tema se describe cómo crear una clave maestra de base de datos en la `master` base de datos de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] .

**En este tema**

- **Antes de empezar:**

  [Seguridad](#Security)

- [Para crear una clave maestra de base de datos mediante Transact-SQL](#TsqlProcedure)

## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar

### <a name="security"></a><a name="Security"></a> Seguridad

#### <a name="permissions"></a><a name="Permissions"></a> Permisos

Necesita el permiso CONTROL en la base de datos.

## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL

### <a name="to-create-a-database-master-key"></a>Para crear la clave maestra de una base de datos

1. Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos.
2. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **Bases de datos del sistema**, haga clic con el botón derecho en `master` y, después, haga clic en **Nueva consulta**.
4. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
