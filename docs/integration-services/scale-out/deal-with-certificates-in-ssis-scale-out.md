---
title: Tratar con certificados de Sql Server Integration Services horizontalmente | Documentos de Microsoft
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2970b2b2cc7cf30c18a203ebbb92b5418bfc9be5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Tratar con certificados de SQL Server Integration Services horizontalmente

Para proteger la comunicación entre escala Out maestra y de escala Out trabajo, se utilizan dos certificados en horizontalmente, es decir, escala Out Master y escala Out trabajo certificado. 

## <a name="scale-out-master-certificate"></a>Certificado de escala Out Master

En la mayoría de los casos, el certificado de escala Out maestra se configura durante la instalación de escala Out Master.

En el **escala Out configuración de Integration Services - nodo Master** página del Asistente para instalación de SQL Server, puede elegir crear un nuevo certificado SSL autofirmado o usar un certificado SSL existente.

![Configuración de master](media/master-config.PNG)

Si no tiene requisitos especiales en certificados, puede crear un nuevo certificado SSL autofirmado. También puede especificar el CNs en el certificado. Asegúrese de que el nombre de host del punto de conexión principal utilizado por escala Out trabajador más adelante se incluye en el CNs. De forma predeterminada, se incluyen el nombre del equipo y la dirección ip del nodo principal. 

Si decide usar un certificado existente, haga clic en "Examinar" para seleccionar un certificado SSL de **raíz** almacén de certificados del equipo local.

### <a name="change-scale-out-master-certificate"></a>Cambiar escala Out Master certificado

Puede que desee cambiar el certificado de escala Out maestra debido a la expiración de certificados u otras razones. Siga los pasos siguientes:

#### <a name="1-create-a-ssl-certificate"></a>1. Cree un certificado SSL.
Cree e instale un certificado SSL en el maestro de nodo con el siguiente comando:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Ejemplo:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Enlazar el certificado al maestro de puerto
Compruebe el enlace original con el comando:
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
Ejemplo:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
Eliminar el enlace original y configurar el nuevo enlace con los siguientes comandos:
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
Ejemplo:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Archivo de configuración de servicio de actualización escala Out Master
Archivo de configuración del servicio de actualización escala Out Master, \<controlador\>: \Program Server\140\DTS\Binn\MasterSettings.config SQL, en patrón de nodo. Actualización **SSLCertThumbprint** a la huella digital del certificado SSL nuevo.

#### <a name="4-restart-scale-out-master-service"></a>4. Reinicie el servicio de escala Out Master

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Volver a conectar escalada de trabajo para escalar horizontalmente Master
Para cada trabajo escala Out, ya sea eliminar el trabajo y vuelva a agregarlo con [escala Out Manager](integration-services-ssis-scale-out-manager.md) o siga los pasos 5.1 a 5.3 siguientes:

5.1 instale el certificado de cliente SSL en el almacén raíz del equipo local en el nodo de trabajo

5.2 actualizar escala Out trabajo servicio configuración actualización escala Out trabajo servicio archivo de configuración, \<controlador\>: \Program Server\140\DTS\Binn\WorkerSettings.config SQL, en el nodo de trabajo. Actualización **MasterHttpsCertThumbprint** a la huella digital del certificado SSL nuevo.

5.3 reiniciar escala horizontalmente servicio de trabajo


## <a name="scale-out-worker-certificate"></a>Certificado del escalado Out trabajo

Certificado de escala Out trabajador se genera automáticamente durante la instalación de escala Out trabajo. 

### <a name="change-scale-out-worker-certificate"></a>Cambiar el certificado de escala Out trabajo

En los casos que desea cambiar el certificado del escalado Out trabajo, siga estos pasos.

#### <a name="1-create-a-certificate"></a>1. Crear un certificado
Cree e instale un certificado con el siguiente comando:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Ejemplo:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Instale el certificado de cliente en el almacén raíz del equipo local en el nodo de trabajo

#### <a name="3-give-service-access-to-the-certificate"></a>3. Conceder acceso al servicio para el certificado
Eliminar el certificado antiguo y conceda acceso de servicio de escala Out trabajo para el nuevo certificado con el comando:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Ejemplo:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Archivo de configuración de escala a un trabajo de actualización
Archivo de configuración de servicio de escala a un trabajo de actualización, \<controlador\>: \Program Server\140\DTS\Binn\WorkerSettings.config SQL, en el nodo de trabajo. Actualización **WorkerHttpsCertThumbprint** a la huella digital del nuevo certificado.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Instale el certificado de cliente en el almacén raíz del equipo local en el maestro de nodo

#### <a name="6-restart-scale-out-worker-service"></a>6. Reiniciar servicio escala Out Worker
