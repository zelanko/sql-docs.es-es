---
title: "Utilizar ADO para publicación en Internet | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1cf73843e742254e9fcbc71299fa1494a669164
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="using-ado-for-internet-publishing"></a>Utilizar ADO para publicación en Internet
[El proveedor OLE DB para Internet Publishing](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) muestra un ejemplo concreto de obtener acceso a datos heterogéneos con ADO. Aunque los ejemplos de esta sección va a ser específicos para utilizar el proveedor de publicación en Internet, los principios que muestran deberían ser similares al usar ADO con otros proveedores de datos heterogéneos, tales como un proveedor a un almacén de correo electrónico.  
  
## <a name="urls"></a>direcciones URL  
 Localizadores uniformes de recursos (URL) puede utilizarse como alternativa a las cadenas de conexión y el texto de comando para especificar los orígenes de datos y la ubicación de archivos y directorios. Puede usar direcciones URL con la existente [conexión](../../../ado/reference/ado-api/connection-object-ado.md) y **Recordset** objetos y con el **registro** y **flujo** objetos.  
  
 Para obtener más información acerca de cómo usar las direcciones URL, vea [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="record-fields"></a>Campos de registro  
 La diferencia distintiva entre datos heterogéneos y los datos homogéneos es que en el primer caso, cada fila de datos, o **registro**, puede tener un conjunto diferente de columnas, o **campos**. Para datos homogéneos, cada fila tiene el mismo conjunto de columnas. Para obtener más información acerca de los campos específicos del proveedor de publicación en Internet, consulte [registros y campos adicionales proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
### <a name="appending-new-fields"></a>Anexar nuevos campos  
 Se han mejorado varios objetos de ADO para trabajar junto con **registro** y **flujo** objetos.  
  
-   El [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección [anexado](../../../ado/reference/ado-api/append-method-ado.md) método, que crea y agrega un [campo](../../../ado/reference/ado-api/field-object.md) a la colección de objetos, también puede especificar el valor de la **campo**.  
  
-   El [actualización](../../../ado/reference/ado-api/update-method.md) método finaliza la adición o eliminación de campos a la colección.  
  
-   Como método abreviado y una alternativa a la **anexado** método, puede crear campos asignando un valor a un campo sin definir o eliminado previamente.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [Direcciones URL absolutas y relativas](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [Registros y campos proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Características de ADO para cada versión](../../../ado/guide/ado-history.md)
