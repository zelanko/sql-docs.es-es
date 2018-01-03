---
title: "CreateObject (método) (RDS) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: CreateObject method [ADO]
ms.assetid: dec96be6-0b31-4953-9c9a-e962b5afcd18
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ba9c2d9ee2c2cf0a646155e5d184640d1aa0283b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="createobject-method-rds"></a>CreateObject (método) (RDS)
Crea al proxy para el objeto de comercial de destino y devuelve un puntero a ella. El proxy empaqueta y ordena datos para el código auxiliar de servidor para las comunicaciones con el objeto de negocios enviar solicitudes y datos a través de Internet. Para los objetos de componente en proceso, se utiliza ningún proxy, se proporciona solo un puntero al objeto.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxis  
 Servicio de datos remoto admite los protocolos siguientes: HTTP, HTTPS (HTTP a través de capa de sockets seguros), DCOM y en proceso.  
  
|Protocolo|Sintaxis|  
|--------------|------------|  
|HTTP|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "http://awebsrvr")|  
|HTTPS|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "https://awebsrvr")|  
|DCOM|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "computername")|  
|En curso|Objeto de conjunto = DataSpace.CreateObject ("ProgId", "")|  
  
## <a name="parameters"></a>Parámetros  
 *Objeto*  
 Una variable de objeto que se evalúa como un objeto que es el tipo especificado en *ProgID*.  
  
 *Espacio de datos*  
 Una variable de objeto que representa un [RDS. DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objeto utilizado para crear una instancia del nuevo objeto.  
  
 *Id. de programa*  
 A **cadena** valor que contiene el identificador de programación que se especifica un objeto comercial de servidor que implementa las reglas de negocios de su aplicación.  
  
 *awebsrvr* o *NombreDeEquipo*  
 A **cadena** valor que representa una dirección URL de identificación del servidor Web de Internet Information Services (IIS) donde se crea una instancia del objeto de negocio de servidor.  
  
## <a name="remarks"></a>Comentarios  
 El *protocolo HTTP* es el protocolo Web estándar; *HTTPS* es un protocolo Web seguro. Use la *protocolo DCOM* cuando ejecute una red de área local sin HTTP. El *en curso* protocolo es una biblioteca de vínculos dinámicos (DLL) local; no usa una red.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto DataFactory, método de consulta y ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)   
 [DataSpace y el ejemplo del método CreateObject (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)   
 [Ejemplo del método CreateRecordset (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)


