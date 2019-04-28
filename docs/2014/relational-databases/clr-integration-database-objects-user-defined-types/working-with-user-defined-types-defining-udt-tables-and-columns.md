---
title: Definir columnas y tablas UDT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 1b87e497c6610a2d75daa9432246e4f4b4690bab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874448"
---
# <a name="defining-udt-tables-and-columns"></a>Definir tablas y columnas de UDT
  Una vez que el ensamblado que contiene el tipo definido por el usuario (UDT) se ha registrado la definición en un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, se puede utilizar en una definición de columna.  
  
## <a name="creating-tables-with-udts"></a>Crear tablas con UDT  
 No hay ninguna sintaxis especial para crear una columna UDT de una tabla. Puede utilizar el nombre del UDT en una definición de columna como si fuera uno de los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intrínsecos. CREATE TABLE siguiente [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción crea una tabla denominada **puntos**, con una columna denominada **ID,** que se define como un `int` columna de identidad y \ la clave principal de la tabla. La segunda columna se denomina **PointValue**, con un tipo de datos de **punto**. El nombre de esquema utilizado en este ejemplo es **dbo**. Observe que debe tener los permisos necesarios para especificar un nombre de esquema. Si omite el nombre de esquema, se utiliza el esquema predeterminado para el usuario de la base de datos.  
  
```  
CREATE TABLE dbo.Points   
(ID int IDENTITY(1,1) PRIMARY KEY, PointValue Point)  
```  
  
## <a name="creating-indexes-on-udt-columns"></a>Crear índices en columnas UDT  
 Hay dos opciones para indizar una columna UDT:  
  
-   Indizar el valor completo. En este caso, si el UDT es binario ordenado, puede crear un índice sobre la columna UDT completa utilizando la instrucción CREATE INDEX de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   Indizar las expresiones UDT. Puede crear los índices en las columnas calculadas mantenidas en las expresiones UDT. La expresión UDT puede ser un campo, método o propiedad de un UDT. La expresión debe ser determinista y no realizar el acceso a los datos.  
  
 Para obtener más información, consulte [Defined tipos](clr-user-defined-types.md) y [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con tipos definidos por el usuario en SQL Server](working-with-user-defined-types-in-sql-server.md)  
  
  
