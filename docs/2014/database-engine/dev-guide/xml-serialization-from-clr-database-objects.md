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
manager: craigg
ms.openlocfilehash: 646d15dc3091323e6e7db2af757640122fb2f0fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779784"
---
# <a name="xml-serialization-from-clr-database-objects"></a>Serialización XML de objetos de base de datos de CLR
  La serialización XML se requiere para dos situaciones:  
  
-   Invocar los servicios web desde los objetos de Common Language Runtime (CLR).  
  
-   Convertir un tipo definido por el usuario (UDT) en XML.  
  
 La realización de la serialización XML invocando la clase `XmlSerializer` genera normalmente un ensamblado de serialización adicional que se sobrecarga en el proyecto con el ensamblado de origen. Sin embargo, por razones de seguridad, esta sobrecarga está deshabilitada en CLR. Por lo tanto, para llamar a un servicio web o realizar la conversión de UDT a XML en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe crear el ensamblado manualmente mediante una herramienta denominada **Sgen.exe** proporcionado con .NET Framework que genera las necesarias ensamblados de serialización. Al invocar `XmlSerializer`, se debe crear el ensamblado de serialización manualmente siguiendo estos pasos:  
  
1.  Ejecute el **Sgen.exe** herramienta proporcionada con el SDK de .NET Framework para crear el ensamblado que contiene los serializadores XML para el ensamblado de origen.  
  
2.  Registre el ensamblado generado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la instrucción `CREATE ASSEMBLY`.  
  
 Para obtener información sobre los errores que puede recibir al realizar la serialización XML, vea el artículo de Microsoft Support siguiente: ["No se puede cargar el ensamblado de serialización generado dinámicamente"](https://support.microsoft.com/kb/913668).  
  
 Para obtener información sobre los tipos de datos no admitidos por XMLSerializer, consulte Compatibilidad con enlaces del esquema XML en .NET Framework en la documentación de .NET Framework.  
  
## <a name="see-also"></a>Vea también  
 [Acceso a datos desde objetos de base de datos CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)   
 [CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)  
  
  
