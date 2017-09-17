---
title: Habilitar una biblioteca DLL para que funcione en DCOM | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e2d67a595c97547934b04794f036d58445e8c282
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitar una biblioteca DLL para que se ejecute en DCOM
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Los pasos siguientes describen cómo habilitar una .dll de objeto de negocios utilizar DCOM y servicios de Microsoft Internet Information Services (HTTP) a través de servicios de componentes.  
  
1.  Crear un nuevo paquete vacío en el complemento MMC Servicios de componentes.  
  
     Utilizará el complemento MMC Servicios de componentes para crear un paquete y agregar el archivo DLL en este paquete. Esto hace que el archivo .dll esté accesible a través de DCOM, pero elimina la accesibilidad a través de IIS. (Si comprueba en el registro para el archivo .dll, el **Inproc** clave ahora está vacía; al establecer el atributo de activación, que se explica más adelante en este tema, se agrega un valor en el **Inproc** clave.)  
  
2.  Instale un objeto de negocios en el paquete.  
  
     -O bien-  
  
     Importar la [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto en el paquete.  
  
3.  Establezca el atributo de activación para que el paquete **en el proceso del creador** (aplicación de biblioteca).  
  
     Para que el archivo .dll sea accesible a través de DCOM e IIS en el mismo equipo, debe establecer los atributos de activación del componente en el complemento MMC Servicios de componentes. Después de establecer el atributo en **en el proceso del creador**, observará que un **Inproc** clave de servidor en el registro se ha agregado que apunta a los servicios de componente .dll sustituta.  
  
 Para obtener más información acerca de servicios de componentes (o Microsoft Transaction Service, si está utilizando Windows NT) y cómo realizar estos pasos, visite el sitio Web de Microsoft Transaction Server.



