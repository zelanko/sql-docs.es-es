---
title: Habilitación de un archivo DLL y ejecutarlo en DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ccfb1189e0c4d9bb0b1684ac3fd47709f491cd48
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704558"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitación de un archivo DLL para ejecutarlo en DCOM
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Los siguientes pasos describen cómo habilitar un archivo .dll de objeto de negocios utilizar DCOM y Microsoft Internet Information Services (HTTP) a través de servicios de componentes.  
  
1.  Crear un nuevo paquete vacío en el complemento MMC Servicios de componentes.  
  
     Usará el complemento MMC Servicios de componentes para crear un paquete y agregar el archivo DLL en este paquete. Esto hace que el archivo .dll que sea accesible a través de DCOM, pero elimina la accesibilidad a través de IIS. (Si comprueba en el registro para el archivo .dll, el **Inproc** clave ahora está vacía; establecer el atributo de activación, se explica más adelante en este tema, se agrega un valor en el **Inproc** clave.)  
  
2.  Instale un objeto de negocios en el paquete.  
  
     -o bien-  
  
     Importar el [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto en el paquete.  
  
3.  Establezca el atributo de activación para que el paquete **en el proceso del creador** (aplicación de biblioteca).  
  
     Para que el archivo .dll accesibles mediante DCOM e IIS en el mismo equipo, debe establecer el atributo de activación del componente en el complemento MMC Servicios de componentes. Después de establecer el atributo en **en el proceso del creador**, observará que un **Inproc** se ha agregado la clave de servidor en el registro que apunta a los servicios de un componente .dll sustituta.  
  
 Para obtener más información acerca de los servicios de componentes (o transacción de servicio de Microsoft, si está utilizando Windows NT) y cómo realizar estos pasos, visite el sitio Web de Microsoft Transaction Server.


