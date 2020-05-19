---
title: Consideraciones de seguridad de diagrama (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- security [SQLXML], updategrams
- updategrams [SQLXML], security
ms.assetid: 00dc6cf4-a2e8-4cca-bdd6-d5122102a82d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a9ed4aad31f5a4697a268d82e282a135ea85c37c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717575"
---
# <a name="updategram-security-considerations-sqlxml-40"></a>Consideraciones de seguridad sobre los diagramas de actualización (SQLXML 4.0)
  A continuación, se muestran una serie de instrucciones de seguridad para usar diagramas de actualización:  
  
-   Evite el uso de la asignación predeterminada cuando utilice los diagramas de actualización para actualizar datos. Cuando se utiliza la asignación predeterminada, un nombre de elemento de un diagrama de actualización se asigna a un nombre de tabla y un nombre de atributo se asigna a una columna. De esta forma, la información de la columna y la tabla de base de datos se expone en la base de datos, lo que puede suponer un riesgo potencial para la seguridad. En lugar de ello, si especifica un esquema de asignación independiente que asigne los elementos y atributos de un diagrama de actualización a las columnas y las tablas de base de datos, los nombres de los atributos y los elementos del diagrama de actualización pueden ser arbitrarios y el esquema realiza la asignación necesaria de estos nombres a las columnas y las tablas de base de datos. Así, la información de la base de datos no se expone en un diagrama de actualización.  
  
-   No permita que los usuarios creen y ejecuten sus diagramas de actualización. Es recomendable que los diagramas de actualización residan como plantillas en un servidor en lugar de crearlos dinámicamente en aplicaciones de tipo ASP, lo que podría poner en peligro los datos de la base de datos. Permitir que los usuarios obtengan acceso a los datos solamente a través de los diagramas de actualización, suministrados como plantillas, puede eliminar este riesgo.  
  
## <a name="see-also"></a>Consulte también  
 [Utilizar los diagramas de actualización para modificar datos en SQLXML 4.0](../updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
  
  
