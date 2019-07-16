---
title: El proveedor OLE DB para la publicación en Internet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 80a373196f98a964bc3e522cc9329907a3392b95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923904"
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>El proveedor OLE DB para la publicación en Internet
ADO [registro](../../../ado/reference/ado-api/record-object-ado.md) y [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objetos pueden utilizarse con el proveedor Microsoft OLE DB para la publicación en Internet (Internet Publishing Provider) para obtener acceso y manipular los recursos, como archivos o carpetas de Web proporcionados por Microsoft FrontPage. Con ADO, puede especificar el origen de un **registro**, **Stream**, o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sea una dirección URL. Puede, a continuación, cargar, descargar, mover, copiar y eliminar recursos o manipular directamente las propiedades de recursos.  
  
 Por ejemplo de código que usa **registros** y **secuencias** con el proveedor de publicación en Internet, consulte el [escenario de publicación en Internet](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 El proveedor de publicación en Internet se instala con Microsoft Windows 2000. Las versiones anteriores del proveedor de publicación en Internet también están disponibles con Microsoft Office 2000 y Microsoft Internet Explorer 5.0.  
  
 Hay tres maneras de conectar ADO con el proveedor de publicación en Internet:  
  
-   Especifique "URL =" en la cadena de conexión. Por ejemplo:  
  
    ```  
    objConn.Open "URL=https://servername"  
    ```  
  
-   Especifique Msdaipp.dso para la *proveedor* palabra clave de la cadena de conexión. Por ejemplo:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=https://servername"  
    ```  
  
-   Especifique Msdaipp.dso para la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Por ejemplo:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "https://servername"  
    ```  
  
> [!NOTE]
>  Si se especifica explícitamente Msdaipp.dso como valor del proveedor, ya sea con la *proveedor* palabra clave de cadena de conexión o la **proveedor** propiedad, no se puede usar "URL =" en la cadena de conexión. Si lo hace, se producirá un error. En su lugar, simplemente especifique la dirección URL como se mostró anteriormente.  
  
 Para obtener información más específica acerca del proveedor de publicación en Internet, consulte [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), o la documentación del proveedor proporcionada con la aplicación de origen con la que el proveedor OLE DB para Se instaló la publicación en Internet: Windows 2000, Office 2000 o Internet Explorer 5.0.
