---
title: Modificar un ensamblado | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], modifying
- permissions [CLR integration]
- altering assemblies
- ALTER ASSEMBLY statement
ms.assetid: 9e765fbd-f339-473c-8537-22f478e79696
author: rothja
ms.author: jroth
ms.openlocfilehash: c22ca979675d3b7f263e3bc6de0c41c134a1abcf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953886"
---
# <a name="altering-an-assembly"></a>Modificar un ensamblado
  Los ensamblados registrados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se pueden actualizar con una versión más reciente mediante la instrucción ALTER ASSEMBLY. Para actualizar un ensamblado, use la instrucción ALTER ASSEMBLY con la sintaxis siguiente:  
  
```  
ALTER ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
```  
  
 ALTER ASSEMBLY no interrumpe los procesos actualmente en ejecución que utilizan el ensamblado; los procesos se siguen ejecutando con el ensamblado sin modificar. ALTER ASSEMBLY no se puede utilizar para cambiar las firmas de funciones de Common Language Runtime (CLR), funciones de agregado, procedimientos almacenados ni desencadenadores. En el ensamblado se pueden agregar nuevos métodos públicos, los métodos privados se pueden modificar de todas las maneras y los métodos públicos se pueden modificar en tanto no se cambien las firmas ni los atributos. Los campos que forman parte de un tipo definido por el usuario de serialización nativa, incluidos los miembros de datos o clases base, no pueden cambiarse mediante ALTER ASSEMBLY. No se admiten otros cambios. Para obtener más información, vea [ALTER assembly &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
## <a name="changing-the-permission-set-of-an-assembly"></a>Cambiar el conjunto de permisos de un ensamblado  
 El conjunto de permisos de un ensamblado también se puede cambiar mediante la instrucción ALTER ASSEMBLY. La instrucción siguiente cambia el conjunto de permisos del ensamblado SQLCLRTest a `EXTERNAL_ACCESS`.  
  
```  
ALTER ASSEMBLY SQLCLRTest  
WITH PERMISSION_SET = EXTERNAL_ACCESS   
```  
  
 Si el conjunto de permisos de un ensamblado se cambia de `SAFE` a `EXTERNAL_ACCESS` o `UNSAFE`, se debe crear previamente una clave asimétrica y el inicio de sesión correspondiendo con permiso `EXTERNAL ACCESS ASSEMBLY` o `UNSAFE ASSEMBLY` para el ensamblado. Para más información, consulte [Creating an Assembly](creating-an-assembly.md).  
  
## <a name="adding-the-source-code-of-an-assembly"></a>Agregar el código fuente de un ensamblado  
 La cláusula ADD FILE de la sintaxis ALTER ASSEMBLY no está presente en CREATE ASSEMBLY. Puede usarla para agregar código fuente o cualquier otro archivo asociado a un ensamblado. Los archivos se copian desde sus ubicaciones originales y se almacenan en tablas del sistema en la base de datos. De esta forma, se garantiza que el código fuente u otros archivos estén disponibles siempre que sea necesario volver a crear o documentar la versión actual del UDT.  
  
 La instrucción siguiente agrega el código fuente de clase Point.cs al UDT Point. De esta forma, el texto incluido en el archivo Point.cs se copia y se almacena en la base de datos con el nombre "PointSource".  
  
 `ALTER ASSEMBLY Point`  
  
 `ADD FILE FROM 'C:\Projects\Point\Point.cs' AS PointSource`  
  
## <a name="see-also"></a>Consulte también  
 [Administrar ensamblados de integración CLR](managing-clr-integration-assemblies.md)   
 [Crear un ensamblado](creating-an-assembly.md)   
 [Quitar un ensamblado](dropping-an-assembly.md)   
 [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql)  
  
  
