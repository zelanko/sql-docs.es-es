---
title: Método CreateObject (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d331bdf617e2b7b748039d69347f00f7fb4046a1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47761224"
---
# <a name="createobject-method-rds"></a>CreateObject (método) (RDS)
Crea al proxy para el objeto de negocios de destino y devuelve un puntero a él. El proxy paquetes y ordena los datos en el código auxiliar del lado servidor para las comunicaciones con el objeto de negocios enviar solicitudes y datos a través de Internet. Para los objetos del componente en proceso, se utiliza ningún proxy, se proporciona solo un puntero al objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Servicio de datos remoto admite los siguientes protocolos: HTTP, HTTPS (HTTP sobre capa de sockets seguros), DCOM y en proceso.  
  
|Protocolo|Sintaxis|  
|--------------|------------|  
|HTTP|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "http://awebsrvr")|  
|HTTPS|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "https://awebsrvr")|  
|DCOM|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "computername")|  
|En curso|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>Parámetros  
 *Objeto*  
 Una variable de objeto que se evalúa como un objeto que es del tipo especificado en *ProgID*.  
  
 *Espacio de datos*  
 Una variable de objeto que representa un [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto utilizado para crear una instancia del nuevo objeto.  
  
 *Id. de programa*  
 Un **cadena** valor que contiene el identificador de programación que se especifica un objeto de negocios de servidor que implementa las reglas de negocios de la aplicación.  
  
 *awebsrvr* o *computername*  
 Un **cadena** valor que representa una dirección URL que identifica el servidor Web de Internet Information Services (IIS) donde se crea una instancia del objeto de negocios del servidor.  
  
## <a name="remarks"></a>Comentarios  
 El *protocolo HTTP* es el protocolo Web estándar; *HTTPS* es un protocolo Web seguro. Use la *protocolo DCOM* cuando se ejecuta una red de área local sin HTTP. El *en proceso* protocolo es una biblioteca de vínculos dinámicos (DLL) local; no utiliza una red.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataFactory, método de consulta y ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace y el ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Ejemplo del método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


