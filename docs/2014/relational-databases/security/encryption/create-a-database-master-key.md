---
title: Creación de una clave maestra de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 757b6c62d63da2b8f1fa33e5d704d7a2c4fabd38
ms.sourcegitcommit: 5a61854ddcd2c61bb6da30ccad68f0ad90da0c96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2019
ms.locfileid: "70978366"
---
# <a name="create-a-database-master-key"></a>Crear la clave maestra de una base de datos

En este tema se describe cómo crear una clave maestra de base `master` de datos [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] en la [!INCLUDE[tsql](../../../includes/tsql-md.md)]base de datos de mediante.

**En este tema**

- **Antes de empezar:**

  [Seguridad](#Security)

- [Para crear una clave maestra de base de datos mediante Transact-SQL](#TsqlProcedure)

## <a name="BeforeYouBegin"></a> Antes de comenzar

### <a name="Security"></a> Seguridad

#### <a name="Permissions"></a> Permisos

Necesita el permiso CONTROL en la base de datos.

## <a name="TsqlProcedure"></a> Usar Transact-SQL

### <a name="to-create-a-database-master-key"></a>Para crear la clave maestra de una base de datos

1. Elija una contraseña para cifrar la copia de la clave maestra que se almacenará en la base de datos.
2. En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].
3. Expanda **bases de datos del sistema**, haga `master` clic con el botón secundario y, a continuación, haga clic en **nueva consulta**.
4. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

Para obtener más información, vea [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql).
