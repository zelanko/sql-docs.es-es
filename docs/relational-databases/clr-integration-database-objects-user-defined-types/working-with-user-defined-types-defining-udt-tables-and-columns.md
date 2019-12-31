---
title: Definir tablas y columnas UDT | Microsoft Docs
ms.custom: ''
ms.date: 12/05/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- user-defined types [CLR integration], columns
- UDTs [CLR integration], columns
- columns [CLR integration]
- user-defined types [CLR integration], tables
- tables [CLR integration]
- UDTs [CLR integration], tables
- UDTs [CLR integration], indexes
- user-defined types [CLR integration], indexes
- indexes [CLR integration]
ms.assetid: aea495f4-ce26-4952-b019-38f012625f3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 8386da85d22f50b45492ecd52588e6d06fe80590
ms.sourcegitcommit: 0d34b654f0b3031041959e87f5b4d4f0a1af6a29
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2019
ms.locfileid: "74901954"
---
# <a name="working-with-user-defined-types---defining-udt-tables-and-columns"></a>Trabajar con tipos definidos por el usuario: definir columnas y tablas UDT
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Una vez que el ensamblado que contiene la definición de tipo definido por el usuario (UDT [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ) se ha registrado en una base de datos, se puede utilizar en una definición de columna. Para más información, consulte [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md).  
  
## <a name="creating-tables-with-udts"></a>Crear tablas con UDT  
 No hay ninguna sintaxis especial para crear una columna UDT de una tabla. Puede utilizar el nombre del UDT en una definición de columna como si fuera uno de los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intrínsecos. La siguiente instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE crea una tabla denominada **Points**, con una columna denominada **ID,** que se define como una columna de identidad **int** y la clave principal de la tabla. La segunda columna se denomina **PointValue**, con un tipo de datos **Point**. El nombre de esquema que se usa en este ejemplo es **DBO**. Observe que debe tener los permisos necesarios para especificar un nombre de esquema. Si omite el nombre de esquema, se utiliza el esquema predeterminado para el usuario de la base de datos.  
  
```sql  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Crear índices en columnas UDT  
 Hay dos opciones para indizar una columna UDT:  
  
-   **Indizar el valor completo.** En este caso, si el UDT es binario ordenado, puede crear un índice sobre la columna UDT completa utilizando la instrucción CREATE INDEX de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Indizar las expresiones UDT.** Puede crear los índices en las columnas calculadas mantenidas en las expresiones UDT. La expresión UDT puede ser un campo, método o propiedad de un UDT. La expresión debe ser determinista y no realizar el acceso a los datos.  
  
 Para obtener más información, vea [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>Véase también  
 [Trabajar con tipos definidos por el usuario en SQL Server](../../relational-databases/clr-integration-database-objects-user-defined-types/working-with-user-defined-types-in-sql-server.md)     
 [CREATE TYPE (Transact-SQL)](../../t-sql/statements/create-type-transact-sql.md)     
 [Tipos definidos por el usuario CLR](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md)     
