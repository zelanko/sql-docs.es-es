---
title: Serialización XML de objetos de base de datos CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
helpviewer_keywords:
- serialization
- XML serialization [CLR integration]
- common language runtime [SQL Server], XML serialization
- XmlSerializer class
ms.assetid: ac84339b-9384-4710-bebc-01607864a344
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ee93ee4b7bf9cba3f11b329244d4523636cb7704
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933146"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Serialización XML de objetos de base de datos de CLR
  La serialización XML se requiere para dos situaciones:  
  
-   Invocar los servicios web desde los objetos de Common Language Runtime (CLR).  
  
-   Convertir un tipo definido por el usuario (UDT) en XML.  
  
 La realización de la serialización XML invocando la clase `XmlSerializer` genera normalmente un ensamblado de serialización adicional que se sobrecarga en el proyecto con el ensamblado de origen. Sin embargo, por razones de seguridad, esta sobrecarga está deshabilitada en CLR. Por lo tanto, para llamar a un servicio web o realizar la conversión de UDT a XML dentro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de, el ensamblado se debe crear manualmente mediante una herramienta denominada **Sgen.exe** proporcionado con el .NET Framework que genera los ensamblados de serialización necesarios. Al invocar `XmlSerializer`, se debe crear el ensamblado de serialización manualmente siguiendo estos pasos:  
  
1.  Ejecute la herramienta de **Sgen.exe** que se proporciona con el SDK de .NET Framework para crear el ensamblado que contiene los serializadores XML para el ensamblado de origen.  
  
2.  Registre el ensamblado generado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la instrucción `CREATE ASSEMBLY`.  
  
 Para obtener información sobre los errores que puede recibir al realizar la serialización XML, vea el siguiente artículo de Soporte técnico de Microsoft: ["no se puede cargar el ensamblado de serialización generado dinámicamente"](https://support.microsoft.com/kb/913668).  
  
 Para obtener información sobre los tipos de datos no admitidos por XMLSerializer, consulte Compatibilidad con enlaces del esquema XML en .NET Framework en la documentación de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Acceso a datos desde objetos de base de datos CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
