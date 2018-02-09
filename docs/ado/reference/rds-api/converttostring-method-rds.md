---
title: "Método ConvertToString (RDS) | Documentos de Microsoft"
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
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95425c734f254bf534eacdad606025fca43c2158
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="converttostring-method-rds"></a>Método ConvertToString (RDS)
Convierte un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) en una cadena MIME que representa los datos del conjunto de registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *DataFactory*  
 Una variable de objeto que representa un [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Recordset*  
 Una variable de objeto que representa un **Recordset** objeto.  
  
## <a name="remarks"></a>Comentarios  
 Con archivos .asp, utilice **ConvertToString** para incrustar el **Recordset** en una página HTML generada en el servidor para su transmisión a un equipo cliente.  
  
 **ConvertToString** carga por primera vez el **Recordset** en el servicio de cursores de las tablas y, a continuación, genera una secuencia en formato MIME.  
  
 En el cliente, servicio de datos remoto puede convertir la cadena MIME en totalmente funcional **conjunto de registros**. Funciona bien cuando se manipulan menos de 400 filas de datos con no más de ancho de 1024 bytes por fila. No debe usar para transmitir datos BLOB y grandes conjuntos de resultados a través de HTTP. No hay compresión de la conexión se realiza en la cadena, muy grandes conjuntos de datos tardará bastante tiempo al transporte a través de HTTP cuando se compara con el formato de tablagrama optimizada definido e implementado por el servicio de datos remotos como su formato de protocolo de transporte nativo.  
  
> [!NOTE]
>  Si está utilizando páginas Active Server para incrustar la cadena MIME resultante en una página HTML de cliente, tenga en cuenta que las versiones anteriores a la versión 2.0 de VBScript limitan el tamaño de la cadena a 32K. Si se supera este límite, se devuelve un error. Mantenga el ámbito de la consulta relativamente pequeño cuando se usa la incrustación MIME a través de los archivos .asp. Para solucionar este problema, descargue la última versión de VBScript desde el sitio Web de Microsoft Windows Script Technologies.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método ConvertToString (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [Ejemplo del método ConvertToString (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


