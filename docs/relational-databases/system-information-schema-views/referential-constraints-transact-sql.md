---
title: REFERENTIAL_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- REFERENTIAL_CONSTRAINTS
- REFERENTIAL_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.REFERENTIAL_CONSTRAINTS view
- REFERENTIAL_CONSTRAINTS view
ms.assetid: 5d358f18-0a85-4b55-af4b-98d5f4cd1020
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f0cb0110e6f2cc047ca5db5f2813b250567573fc
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132145"
---
# <a name="referentialconstraints-transact-sql"></a>REFERENTIAL_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada restricción FOREIGN KEY de la base de datos actual. Esta vista de esquema de información devuelve información acerca de los objetos para los que el usuario actual tiene permisos.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Calificador de la restricción.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la restricción.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nombre de la restricción.|  
|**UNIQUE_CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Calificador de la restricción UNIQUE.|  
|**UNIQUE_CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la restricción UNIQUE.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**UNIQUE_CONSTRAINT_NAME**|**sysname**|Restricción UNIQUE.|  
|**MATCH_OPTION**|**varchar (** 7 **)**|Condiciones de coincidencia de restricción referencial. Siempre devuelve SIMPLE. Esto significa que no se define ninguna coincidencia. La condición se considera una coincidencia en una de las siguientes circunstancias:<br /><br /> Al menos un valor de la columna de clave externa es NULL.<br /><br /> Ninguno de los valores de la columna de clave externa es NULL y una fila de la tabla de clave principal tiene la misma clave.|  
|**UPDATE_RULE**|**varchar (** 11 **)**|Acción realizada cuando un [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción infringe la integridad referencial definida por esta restricción. Devuelve una de las siguientes opciones: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Si para esta restricción se especifica NO ACTION en ON UPDATE, la actualización de la clave principal a la que se hace referencia en la restricción no se propagará a la clave externa. Si una actualización de una clave principal de estas características provocara una infracción de la integridad referencial porque al menos una clave externa contiene el mismo valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realizará ningún cambio en las tablas primaria y de referencia. Asimismo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un error.<br /><br /> Si para esta restricción se especifica CASCADE en ON UPDATE, cualquier cambio en el valor de clave principal se propagará automáticamente al valor de clave externa.|  
|**DELETE_RULE**|**varchar (** 11 **)**|Acción que se realiza cuando una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] infringe la integridad referencial definida por esta restricción. Devuelve una de las siguientes opciones: <br />NO ACTION<br />CASCADE<br />SET NULL<br />SET DEFAULT<br /><br /> Si para esta restricción se especifica NO ACTION en ON DELETE, la eliminación de la clave principal a la que se hace referencia en la restricción no se propagará a la clave externa. Si una eliminación de una clave principal de estas características provocara una infracción de la integridad referencial porque al menos una clave externa contiene el mismo valor, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realizará ningún cambio en las tablas primaria y de referencia. Asimismo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un error.<br /><br /> Si para esta restricción se especifica CASCADE en ON DELETE, cualquier cambio en el valor de clave principal se propagará automáticamente al valor de clave externa.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [Sys.Foreign_Keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
