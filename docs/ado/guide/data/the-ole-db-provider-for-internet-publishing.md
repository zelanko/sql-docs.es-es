---
title: "El proveedor OLE DB para la publicación en Internet | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLE DB provider for Internet publishing [ADO]
- ADO, Internet publishing
- publishing to Internet [ADO]
- Internet publishing [ADO]
- providers [ADO], OLE DB provider for Internet publishing
ms.assetid: 4869aafa-7401-4ce1-93ce-45406a60274f
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 128d8531f1a5f4c2ebff06b9db8b1510964bdcd4
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="the-ole-db-provider-for-internet-publishing"></a>El proveedor OLE DB para la publicación en Internet
La propiedad ADO [registro](../../../ado/reference/ado-api/record-object-ado.md) y [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objetos pueden utilizarse con el proveedor Microsoft OLE DB para publicación en Internet (Internet Publishing Provider) para tener acceso y manipular los recursos, como archivos o carpetas Web proporcionados por Microsoft FrontPage. Con ADO, puede especificar el origen de un **registro**, **flujo**, o [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) sea una dirección URL. Puede, a continuación, cargar, descargar, mover, copiar y eliminar recursos o manipular directamente las propiedades del recurso.  
  
 Por ejemplo código que usa **registros** y **secuencias** con el proveedor de publicación en Internet, consulte el [escenario de Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md).  
  
 El proveedor de publicación en Internet se instala con Microsoft Windows 2000. Las versiones anteriores de Internet Publishing Provider también están disponibles con Microsoft Office 2000 y Microsoft Internet Explorer 5.0.  
  
 Hay tres maneras de conectar ADO con el proveedor de publicación de Internet:  
  
-   Especifique "URL =" en la cadena de conexión. Por ejemplo:  
  
    ```  
    objConn.Open "URL=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para la *proveedor* palabra clave de la cadena de conexión. Por ejemplo:  
  
    ```  
    objConn.Open "provider=MSDAIPP.DSO;data source=http://servername"  
    ```  
  
-   Especifique Msdaipp.dso para la [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad de la [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto. Por ejemplo:  
  
    ```  
    objConn.Provider = "MSDAIPP.DSO"  
    objConn.Open "http://servername"  
    ```  
  
> [!NOTE]
>  Si se especifica explícitamente Msdaipp.dso como valor del proveedor, ya sea con la *proveedor* palabra clave de cadena de conexión o la **proveedor** propiedad, no se puede utilizar "URL =" en la cadena de conexión. Si lo hace, se producirá un error. En su lugar, simplemente especifique la dirección URL como se muestra anteriormente.  
  
 Para obtener información más específica acerca del proveedor de publicación en Internet, consulte [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md), o la documentación del proveedor proporcionada con la aplicación de origen con el que el proveedor OLE DB para Publicación en Internet se instaló: Windows 2000, Office 2000 o Internet Explorer 5.0.
