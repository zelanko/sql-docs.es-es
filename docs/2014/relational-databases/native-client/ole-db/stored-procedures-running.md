---
title: Ejecutar procedimientos almacenados (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [OLE DB], executing
- OLE DB, stored procedures
- SQL Server Native Client OLE DB provider, stored procedures
ms.assetid: c77d9be9-2176-4438-8c7a-04b63ebece08
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1ddff98bca54c41d94d4d3545d59495a995e1d33
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201578"
---
# <a name="running-stored-procedures-ole-db"></a>Ejecutar procedimientos almacenados (OLE DB)
  Al ejecutar las instrucciones, puede proporcionar una llamada a un procedimiento almacenado en el origen de datos (en lugar de ejecutar o preparar directamente una instrucción en la aplicación cliente):  
  
-   Mayor rendimiento.  
  
-   Sobrecarga de red reducida.  
  
-   Mejor coherencia  
  
-   Mayor exactitud  
  
-   Funcionalidad agregada.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client es compatible con tres de los mecanismos que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan procedimientos almacenados para devolver datos:  
  
-   Cada instrucción SELECT del procedimiento genera un conjunto de resultados.  
  
-   El procedimiento puede devolver datos mediante parámetros de salida.  
  
-   El procedimiento puede tener un código de retorno de tipo entero.  
  
 La aplicación debe ser capaz de manejar todos estos resultados de los procedimientos almacenados.  
  
 Diferentes proveedores OLE DB devuelven parámetros de salida y valores devueltos en diferentes momentos durante el procesamiento de los resultados. En caso de los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB, los parámetros de salida y códigos de retorno no se proporcionan hasta después de que el consumidor haya recuperado o cancelado los conjuntos de resultados devueltos por el procedimiento almacenado. Los códigos de retorno y los parámetros de salida se devuelven en el último paquete TDS del servidor.  
  
 Los proveedores usan la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY para notificar cuando devuelve parámetros de salida y valores de retorno. Esta propiedad se encuentra en el conjunto de propiedades DBPROPSET_DATASOURCEINFO.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client establece la propiedad DBPROP_OUTPUTPARAMETERAVAILABILITY en DBPROPVAL_OA_ATROWRELEASE para indicar que los códigos de retorno y parámetros de salida no se devuelven hasta que se procese o lance el conjunto de resultados.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados](stored-procedures.md)  
  
  