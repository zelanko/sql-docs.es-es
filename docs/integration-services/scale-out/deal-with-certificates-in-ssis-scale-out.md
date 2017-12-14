---
title: Usar certificados en la escalabilidad horizontal de SQL Server Integration Services | Microsoft Docs
ms.custom: 
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: scale-out
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "1"
author: haoqian
ms.author: haoqian
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e09fec1fcf9cf0221dad50d708adef773b297237
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="deal-with-certificates-in-sql-server-integration-services-scale-out"></a>Usar certificados en la escalabilidad horizontal de SQL Server Integration Services

Para proteger la comunicación entre el patrón de escalabilidad horizontal y el trabajo de escalabilidad horizontal, se usan dos certificados en la escalabilidad horizontal; por ejemplo, el certificado del patrón de escalabilidad horizontal y el del trabajo de escalabilidad horizontal. 

## <a name="scale-out-master-certificate"></a>Certificado del patrón de escalabilidad horizontal

En la mayoría de los casos, el certificado del patrón de escalabilidad horizontal se configura durante la instalación de este patrón de escalabilidad horizontal.

En la página **Configuración de la escalabilidad horizontal de Integration Services - Nodo principal** del asistente de instalación de SQL Server, puede elegir crear un nuevo certificado SSL autofirmado o usar un certificado SSL ya existente.

![Configuración principal](media/master-config.PNG)

Si no tiene requisitos especiales en los certificados, puede crear un nuevo certificado SSL autofirmado. Además, puede especificar los nombres comunes en el certificado. Asegúrese de que el nombre de host del punto de conexión del patrón que el trabajo de escalabilidad horizontal usará más adelante se incluye en el apartado de nombres comunes. De forma predeterminada, se incluyen el nombre de la máquina y la dirección IP del nodo principal. 

Si decide usar un certificado existente, haga clic en "Examinar..." para seleccionar un certificado SSL desde el almacén de certificados **raíz** del equipo local.

### <a name="change-scale-out-master-certificate"></a>Cambiar el certificado del patrón de escalabilidad horizontal

Puede que quiera cambiar el certificado del patrón de escalabilidad horizontal porque está a punto de expirar o por otras razones. Para hacerlo, siga estos pasos:

#### <a name="1-create-a-ssl-certificate"></a>1. Cree un certificado SSL.
Cree e instale un certificado SSL en el nodo principal mediante el siguiente comando:
```dos
MakeCert.exe -n CN={master endpoint host} SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```
Ejemplo:
```dos
MakeCert.exe -n CN=MasterMachine SSISScaleOutMaster.cer -r -ss Root -sr LocalMachine
```

#### <a name="2-bind-the-certificate-to-master-port"></a>2. Enlace el certificado al puerto principal.
Compruebe el enlace original mediante el comando:
```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```
Ejemplo:
```dos
netsh http show sslcert ipport=0.0.0.0:8391
```
Elimine el enlace original y configure el nuevo enlace mediante los siguientes comandos:
```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={SSL Certificate Thumbprint} certstorename=Root appid={original appid}
```
Ejemplo:
```dos
netsh http delete sslcert ipport=0.0.0.0:8391
netsh http add sslcert ipport=0.0.0.0:8391 certhash=01d207b300ca662f479beb884efe6ce328f77d53 certstorename=Root appid={a1f96506-93e0-4c91-9171-05a2f6739e13}
```
#### <a name="3-update-scale-out-master-service-configuration-file"></a>3. Actualice el archivo de configuración del servicio del patrón de escalabilidad horizontal.
Actualice el archivo de configuración del servicio del patrón de escalabilidad horizontal (\<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\MasterSettings.config) en el nodo principal. Actualice **SSLCertThumbprint** a la huella digital del certificado SSL nuevo.

#### <a name="4-restart-scale-out-master-service"></a>4. Reinicie el servicio del patrón de escalabilidad horizontal.

#### <a name="5-reconnect-scale-out-worker-to-scale-out-master"></a>5. Reconecte el trabajo y el patrón de escalabilidad horizontal.
En cada trabajo de escalabilidad horizontal, puede optar por eliminar ese trabajo y volver a agregarlo mediante el [Administrador de escalabilidad horizontal](integration-services-ssis-scale-out-manager.md) o seguir los pasos 5.1 a 5.3 que se detallan a continuación:

5.1 Instale el certificado SSL de cliente en el almacén raíz de la máquina local en el nodo del trabajo.

5.2 Actualice el archivo de configuración del servicio de trabajo de escalabilidad horizontal (\<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config), en el nodo de trabajo. Actualice **MasterHttpsCertThumbprint** a la huella digital del certificado SSL nuevo.

5.3 Reinicie el servicio de trabajo de escalabilidad horizontal.


## <a name="scale-out-worker-certificate"></a>Certificado de trabajo de escalabilidad horizontal

El certificado de trabajo de escalabilidad horizontal se crea automáticamente durante la instalación del trabajo de escalabilidad horizontal en cuestión. 

### <a name="change-scale-out-worker-certificate"></a>Cambiar el certificado de trabajo de escalabilidad horizontal

En los casos en que quiera cambiar el certificado del trabajo de escalabilidad horizontal, siga estos pasos.

#### <a name="1-create-a-certificate"></a>1. Crear un certificado
Cree e instale un certificado mediante el siguiente comando:
```dos
MakeCert.exe -n CN={worker machine name};CN={worker machine ip} SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
Ejemplo:
```dos
MakeCert.exe -n CN=WorkerMachine;CN=10.0.2.8 SSISScaleOutWorker.cer -r -ss My -sr LocalMachine
```
#### <a name="2-install-the-client-certificate-to-the-root-store-of-local-machine-on-worker-node"></a>2. Instale el certificado de cliente en el almacén raíz de la máquina local en el nodo del trabajo.

#### <a name="3-give-service-access-to-the-certificate"></a>3. Conceda acceso de servicio al certificado.
Elimine el certificado antiguo y conceda acceso al nuevo certificado al servicio de trabajo de escalabilidad horizontal mediante el comando:
```dos
certmgr.exe /del /c /s /r localmachine My /n {CN of the old certificate}
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the new certificate} -a {the account running Scale Out Worker service}
```
Ejemplo:
```dos
certmgr.exe /del /c /s /r localmachine My /n WorkerMachine
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s WorkerMachine -a SSISScaleOutWorker140
```
#### <a name="4-update-scale-out-worker-configuration-file"></a>4. Actualice el archivo de configuración del trabajo de escalabilidad horizontal.
Actualice el archivo de configuración del servicio del trabajo de escalabilidad horizontal (\<controlador\>:\Archivos de programa\Microsoft SQL Server\140\DTS\Binn\WorkerSettings.config) en el nodo de trabajo. Actualice **WorkerHttpsCertThumbprint** a la huella digital del certificado nuevo.

#### <a name="5-install-the-client-certificate-to-the-root-store-of-local-machine-on-master-node"></a>5. Instale el certificado de cliente en el almacén raíz de la máquina local en el nodo principal.

#### <a name="6-restart-scale-out-worker-service"></a>6. Reinicie el servicio de trabajo de escalabilidad horizontal.
