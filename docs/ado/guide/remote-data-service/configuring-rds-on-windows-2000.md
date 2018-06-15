---
title: Configurar RDS en Windows 2000 | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 774309f4b120f3c475645574429d1b08af627f8b
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35273774"
---
# <a name="configuring-rds-on-windows-2000"></a>Configurar RDS en Windows 2000
Si tiene dificultades para conseguir que RDS funcione correctamente después de actualizar a Windows 2000, siga estos pasos para solucionar el problema:  
  
1.  Asegúrese de que el servicio de publicación World Wide Web se ejecuta primero, vaya a http:// servidor mediante el Explorador de Internet. Si no se puede acceder al servidor de Web de esta manera, abra un símbolo del sistema y escriba el comando siguiente, "NET iniciar W3SVC".  
  
2.  En el menú Inicio, seleccione Ejecutar. Escriba msdfmap.ini y, a continuación, haga clic en Aceptar para abrir el archivo msdfmap.ini en el Bloc de notas. Compruebe la sección [CONNECT DEFAULT] y, si el parámetro de acceso se establece en NOACCESS, cámbielo a READONLY.  
  
3.  Mediante la utilidad RegEdit, navegue hasta el registro hasta "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" y asegúrese de que **HandlerRequired** se establece en 0 y **controlador predeterminado** es "" (cadena nula).  
  
     **Tenga en cuenta** si realiza cambios en esta sección del registro, debe detener y reiniciar el servicio de publicación World Wide Web escribiendo los comandos siguientes en un símbolo del sistema: "NET STOP W3SVC" y "NET iniciar W3SVC".  
  
4.  Con la utilidad RegEdit, navegue en el registro para "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" y compruebe que existe una clave denominada **RDSServer.Datafactory**. De lo contrario, créelo.  
  
5.  Con el Administrador de servicios de Internet, localice el sitio Web predeterminado y ver las propiedades de la raíz virtual MSADC. Inspeccione el directorio seguridad o la dirección IP y las restricciones de nombre de dominio. Si se activa el "acceso denegado", a continuación, seleccione "Concedido".  
  
 No olvide reiniciar el servidor si los cambios no aparezcan solucionar el problema en un primer momento.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Las aplicaciones que utilizan RDS deben migrar a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565). Componentes de servidor RDS a partir de Windows 8 y Windows Server 2012, ya no están incluidos en el sistema operativo Windows. Migrar las aplicaciones que utilizan RDS a [servicio de datos de WCF](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


