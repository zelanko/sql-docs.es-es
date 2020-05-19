---
title: Control de valores NULL (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d21c1a215b05896838c4127c9a35f8add334f713
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703042"
---
# <a name="null-handling-sqlxml-40"></a>Controlar valores NULL (SQLXML 4.0)
  La sintaxis XML indica NULL como una ausencia. (Por ejemplo, si un valor de atributo o elemento es NULL, ese atributo o elemento está ausente del documento XML). En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, el `updg:nullvalue` atributo permite especificar null para un valor de elemento o atributo.  
  
 Por ejemplo, el siguiente diagrama garantiza que el valor de **título** de un contacto con **ContactID** de 64 es NULL y, a continuación, actualiza el valor del **título** a "Mr". para este contacto.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync updg:nullvalue="IsNULL"  >  
    <updg:before>  
       <Person.Contact ContactID="64" Title="IsNULL" />  
    </updg:before>  
    <updg:after>  
       <Person.Contact ContactID="64" Title="Mr." />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Cuando se pasan parámetros a un diagrama de actualización, se puede pasar NULL como valor de parámetro. Esto se hace especificando el atributo `nullvalue` en el bloque `<updg:header>`. Para obtener un ejemplo, vea [pasar parámetros a diagramas &#40;SQLXML 4,0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte también  
 [Consideraciones de seguridad de diagrama &#40;SQLXML 4,0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
