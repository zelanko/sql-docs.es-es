---
title: Método ConvertToString (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 71e50c4f611342c8e06687c47ab1c45fb60974ac
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67964577"
---
# <a name="converttostring-method-rds"></a>Método ConvertToString (RDS)
Convierte un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) en una cadena MIME que representa los datos del conjunto de registros.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
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
  
 En el cliente, el servicio de datos remoto puede convertir la cadena MIME en funcione completamente **Recordset**. Funciona bien para administrar menos de 400 filas de datos con no más de ancho de 1024 bytes por fila. No debe usarlo para transmitir datos BLOB y grandes conjuntos de resultados a través de HTTP. Compresión de la conexión no se realiza en la cadena, muy grandes conjuntos de datos tardará bastante tiempo al transporte a través de HTTP en comparación con el formato optimizado para la conexión tablegram definidas e implementadas por el servicio de datos remotos como su formato de protocolo de transporte nativo.  
  
> [!NOTE]
>  Si usa páginas Active Server para insertar la cadena MIME resultante en una página HTML del cliente, tenga en cuenta que las versiones anteriores a la versión 2.0 de VBScript limitan el tamaño a 32 KB. Si se supera este límite, se devuelve un error. Mantenga el ámbito de la consulta relativamente pequeña cuando se usa la incrustación MIME a través de los archivos .asp. Para solucionar este problema, descargue la última versión de VBScript desde el sitio Web de Microsoft Windows Script Technologies.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo del método ConvertToString (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [Ejemplo del método ConvertToString (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


