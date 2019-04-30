---
title: Configuración de RDS en Windows 2000 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ee1d76052402ab775e9e8de20e1ef6da07e23432
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63214795"
---
# <a name="configuring-rds-on-windows-2000"></a>Configuración de RDS en Windows 2000
Si experimenta dificultades para conseguir que RDS funcione correctamente después de actualizar a Windows 2000, siga estos pasos para solucionar el problema:  
  
1.  Asegúrese de que se ejecuta primero el servicio de publicación World Wide Web, vaya a https:// server mediante el uso de Internet Explorer. Si no puede acceder el servidor Web de esta manera, abra un símbolo del sistema y escriba el comando siguiente, "NET iniciar W3SVC".  
  
2.  En el menú Inicio, seleccione Ejecutar. Escriba msdfmap.ini y, a continuación, haga clic en Aceptar para abrir el archivo msdfmap.ini en el Bloc de notas. Consulte la sección [DEFAULT conectarse] y, si el parámetro de acceso se establece en NOACCESS, cámbielo a READONLY.  
  
3.  Mediante la utilidad RegEdit, vaya a "Registro hasta HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" y asegúrese de que **HandlerRequired** se establece en 0 y **DefaultHandler** es "" (cadena nula).  
  
     **Tenga en cuenta** si realiza cambios en esta sección del registro, debe detener y reiniciar el servicio de publicación World Wide Web escribiendo los siguientes comandos en un símbolo del sistema: "NET STOP W3SVC" y "NET iniciar W3SVC".  
  
4.  Con la utilidad RegEdit, navegue en el registro a "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" y compruebe que existe una clave denominada **RDSServer.Datafactory**. Si no es así, crearla.  
  
5.  Con el Administrador de servicios de Internet, busque el sitio Web predeterminado y ver las propiedades de la raíz virtual MSADC. Inspeccione el directorio seguridad o la dirección IP y las restricciones de nombre de dominio. Si se activa el "acceso denegado", a continuación, seleccione "Granted".  
  
 Asegúrese de reiniciar el servidor si los cambios no aparezcan solucionar el problema en primer lugar.  
  
> [!IMPORTANT]
>  A partir de Windows 8 y Windows Server 2012, componentes de servidor RDS ya no están incluidos en el sistema operativo de Windows (consulte Windows 8 y [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obtener más detalles). Componentes de cliente RDS se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Deben migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565). Componentes de servidor RDS a partir de Windows 8 y Windows Server 2012, ya no se incluyen en el sistema operativo de Windows. Migrar las aplicaciones que usan RDS a [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


