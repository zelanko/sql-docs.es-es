---
title: Utilizar ADO para publicación en Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- urls [ADO]
ms.assetid: d399fce4-b70b-418f-8110-3deb3448863c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ac7922dda2d486f4783d1230296dc89b81cb4fe3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718609"
---
# <a name="using-ado-for-internet-publishing"></a>Utilizar ADO para publicación en Internet
[El proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md) muestra un ejemplo concreto de tener acceso a datos heterogéneos con ADO. Aunque los ejemplos en esta sección serán específicos para usar el proveedor de publicación en Internet, los principios que muestran deben ser similar al usar ADO con otros proveedores de datos heterogéneos, como un proveedor a un almacén de correo electrónico.  
  
## <a name="urls"></a>direcciones URL  
 Localizadores uniformes de recursos (URL) puede utilizarse como alternativa a las cadenas de conexión y el texto de comando para especificar los orígenes de datos y la ubicación de archivos y directorios. Puede usar direcciones URL con el existente [conexión](../../../ado/reference/ado-api/connection-object-ado.md) y **Recordset** objetos y con el **registro** y **Stream** objetos.  
  
 Para obtener más información sobre cómo usar las direcciones URL, vea [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="record-fields"></a>Campos de registro  
 La diferencia distintiva entre datos heterogéneos y los datos homogéneos es que en el primer caso, cada fila de datos, o **registro**, puede tener un conjunto diferente de columnas, o **campos**. Para los datos homogéneos, cada fila tiene el mismo conjunto de columnas. Para obtener más información acerca de los campos específicos del proveedor de publicación en Internet, consulte [registros y campos adicionales proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md).  
  
### <a name="appending-new-fields"></a>Anexar nuevos campos  
 Se han mejorado para trabajar junto con varios objetos de ADO **registro** y **Stream** objetos.  
  
-   El [campos](../../../ado/reference/ado-api/fields-collection-ado.md) colección [Append](../../../ado/reference/ado-api/append-method-ado.md) método, que crea y agrega un [campo](../../../ado/reference/ado-api/field-object.md) a la colección de objetos, también puede especificar el valor de la **campo**.  
  
-   El [actualización](../../../ado/reference/ado-api/update-method.md) método finaliza la adición o eliminación de campos de la colección.  
  
-   Como método abreviado y una alternativa a la **Append** método, puede crear campos asignando un valor a un campo sin definir o eliminado anteriormente.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El proveedor OLE DB para la publicación en Internet](../../../ado/guide/data/the-ole-db-provider-for-internet-publishing.md)  
  
-   [Escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md)  
  
-   [Direcciones URL absolutas y relativas](../../../ado/guide/data/absolute-and-relative-urls.md)  
  
-   [Registros y campos proporcionados por el proveedor](../../../ado/guide/data/records-and-provider-supplied-fields.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Características de ADO para cada versión](../../../ado/guide/ado-history.md)
