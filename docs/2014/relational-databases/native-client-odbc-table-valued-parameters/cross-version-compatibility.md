---
title: Compatibilidad entre versiones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), cross-version compatibility
ms.assetid: 5f14850b-b85c-41e2-8116-6f5b3f5e0856
author: rothja
ms.author: jroth
ms.openlocfilehash: af434713946f5c568ee71644a7403f9496a8c16f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049706"
---
# <a name="cross-version-compatibility"></a>Compatibilidad entre versiones
  Pueden producirse conflictos entre versiones cuando se espera que las instancias cliente o servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] procesen los parámetros con valores de tabla.  
  
 En general, la funcionalidad de los parámetros con valores de tabla solo está disponible para los clientes de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (con SQL Server Native Client 10.0) o posterior que están conectados a los servidores de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior). Las nuevas columnas de los conjuntos de resultados de la función de catálogo solo estarán presentes cuando se conecten a un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] servidor de (o posterior).  
  
 Si una aplicación cliente compilada con una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ejecuta instrucciones que esperan parámetros con valores de tabla, el servidor detecta esta condición a través de un error de conversión de datos y ODBC devuelve esto como SQLSTATE 07006 y el mensaje "Infracción del atributo de tipo de datos restringido".  
  
 Si una aplicación cliente que se compiló con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native client 10,0 o una versión posterior intenta usar parámetros con valores de tabla cuando se conecta a una instancia de servidor anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client lo detectará, y se producirá un error 07006 en las llamadas de tipo de datos restringido (la versión de SQL Server para esta conexión no admite parámetros con valores de tabla) ".  
  
## <a name="see-also"></a>Consulte también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
