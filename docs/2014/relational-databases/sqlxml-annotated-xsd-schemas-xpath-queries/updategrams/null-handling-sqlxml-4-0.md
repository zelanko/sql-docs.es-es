---
title: NULL (SQLXML 4.0) de control | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updg:nullvalue attribute
- updategrams [SQLXML], null values
- nullvalue attribute
- null values [SQLXML]
ms.assetid: 5e11eebb-d94e-4ce6-a6d0-870225706bc1
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fb61234696e419bc203822985f8966a81975e476
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172124"
---
# <a name="null-handling-sqlxml-40"></a>Controlar valores NULL (SQLXML 4.0)
  La sintaxis XML indica NULL como una ausencia. (Por ejemplo, si un valor de atributo o elemento es NULL, ese atributo o elemento está ausente en el documento XML). En [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML, el atributo `updg:nullvalue` permite especificar el valor NULL para un valor de elemento o atributo.  
  
 Por ejemplo, el diagrama de actualización siguiente asegura que el **título** valor de un contacto con **ContactID** de 64 es NULL y, a continuación, actualiza el **título** valor a "MR." para este contacto.  
  
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
  
 Cuando se pasan parámetros a un diagrama de actualización, se puede pasar NULL como valor de parámetro. Esto se hace especificando el atributo `nullvalue` en el bloque `<updg:header>`. Para obtener un ejemplo, vea [pasar parámetros a diagramas de actualización &#40;SQLXML 4.0&#41;](passing-parameters-to-updategrams-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
