---
title: "Solución de problemas de escalabilidad horizontal de SQL Server Integration Services (SSIS) | Microsoft Docs"
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
ms.openlocfilehash: 56d61bc6ba76514ba2291243002a7423ec8e265c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="troubleshooting-scale-out"></a>Solución de problemas de escalabilidad horizontal

La escalabilidad horizontal de SSIS implica la comunicación entre SSISDB, el servicio del patrón de escalabilidad horizontal y el servicio del trabajo de escalabilidad horizontal. A veces, la comunicación se interrumpe debido a errores de configuración, falta de permisos de acceso y otros motivos. Este documento le ayudará a solucionar problemas de configuración de escalabilidad horizontal.

Para investigar los síntomas que experimente, realice los pasos siguientes uno por uno hasta que se resuelva el problema.

### <a name="symptoms"></a>**Síntomas** 
El patrón de escalabilidad horizontal no se puede conectar a SSISDB. 

Las propiedades del patrón no se pueden mostrar en el Administrador de escalabilidad horizontal.

Las propiedades del patrón no se rellenan en [SSISDB].[catalog].[master_properties]

### <a name="solution"></a>**Solución**
Paso 1: Comprobar si la escalabilidad horizontal está habilitada.

Haga clic con el botón derecho en el nodo **SSISDB** en el Explorador de objetos de SSMS y compruebe que la característica **Escalabilidad horizontal esté habilitada**.

![Escalabilidad horizontal habilitada](media\isenabled.PNG)

Si el valor de propiedad es False, habilite Escalabilidad horizontal mediante una llamada al procedimiento almacenado [SSISDB].[catalog].[enable_scaleout].

Paso 2: Comprobar si el nombre de SQL Server especificado en el archivo de configuración del patrón de escalabilidad horizontal es correcto y reiniciar el servicio del patrón de escalabilidad horizontal.

### <a name="symptoms"></a>**Síntomas** 
El trabajo de escalabilidad horizontal no puede conectarse al patrón de escalabilidad horizontal.

El trabajo de escalabilidad horizontal no se muestra después de agregarlo en el Administrador de escalabilidad horizontal

El trabajo de escalabilidad horizontal no se muestra en [SSISDB].[catalog].[worker_agents]

El servicio del trabajo de escalabilidad horizontal se está ejecutando mientras el trabajo de escalabilidad horizontal está desconectado

### <a name="solutions"></a>**Soluciones** 
Compruebe los mensajes de error de registro del servicio de trabajo de escalabilidad horizontal en \<unidad\>:\Usuarios\\*[cuenta que ejecuta el servicio de trabajo]*\AppData\Local\SSIS\Cluster\Agent.

**Caso** 

System.ServiceModel.EndpointNotFoundException: No había ningún punto de conexión escuchando en https://*[NombreDeEquipo]:[Puerto]*/ClusterManagement/ que pudiera aceptar el mensaje.

Paso 1: Comprobar si el número de puerto especificado en el archivo de configuración del servicio del patrón de escalabilidad horizontal es correcto y reiniciar el servicio del patrón de escalabilidad horizontal. 

Paso 2: Comprobar si el punto de conexión principal especificado en la configuración del servicio del trabajo de escalabilidad horizontal es correcto y reiniciar el servicio del trabajo de escalabilidad horizontal.

Paso 3: Comprobar si el puerto de firewall está abierto en el nodo del patrón de escalabilidad horizontal.

Paso 4: Resolver cualquier otro problema de conexión entre el nodo del patrón de escalabilidad horizontal y el nodo del trabajo de escalabilidad horizontal.

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: No se puede establecer una relación de confianza para el canal seguro SSL/TLS con la entidad '*[Nombre de la máquina]:[Puerto]*'. ---> System.Net.WebException. Se cerró la conexión subyacente: No se puede establecer una relación de confianza para el canal seguro SSL/TLS. ---> System.Security.Authentication.AuthenticationException: El certificado remoto no es válido según el procedimiento de validación.

Paso 1: Instalar el certificado del patrón de escalabilidad horizontal para el almacén de certificados raíz de la máquina local en el nodo de trabajo de escalabilidad horizontal si todavía no está instalado y reiniciar el servicio del trabajo de escalabilidad horizontal.

Paso 2: Comprobar si el nombre de host del punto de conexión principal está incluido en los nombres comunes del certificado del patrón de escalabilidad horizontal. Si no es así, restablezca el punto de conexión principal del archivo de configuración del trabajo de escalabilidad horizontal y reinicie el servicio del trabajo de escalabilidad horizontal. 

> [!Note]
> Si no es posible cambiar el nombre de host del punto de conexión principal debido a la configuración de DNS, debe cambiar el certificado del patrón de escalabilidad horizontal. Consulte [Deal with certificates in SSIS Scale Out](deal-with-certificates-in-ssis-scale-out.md) (Tratar con certificados en la escalabilidad horizontal de SSIS)

Paso 3: Comprobar si la huella digital del patrón especificada en la configuración del trabajo de escalabilidad horizontal coincide con el certificado del patrón de escalabilidad horizontal de la huella digital. 

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: No se pudo establecer un canal seguro para SSL/TLS con la autoridad '*[Nombre de la máquina]:[Puerto]*'. ---> System.Net.WebException. Se anuló la solicitud: No se puede crear un canal seguro SSL/TLS.

Paso 1: Comprobar si la cuenta que ejecuta el servicio del trabajo de escalabilidad horizontal tiene acceso al certificado del trabajo de escalabilidad horizontal mediante el siguiente comando.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Si la cuenta no tiene acceso, concédaselo mediante el comando siguiente y reinicie el servicio del trabajo de escalabilidad horizontal.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Caso**

System.ServiceModel.Security.MessageSecurityException: Se prohibió la solicitud HTTP con el esquema de autenticación de cliente 'Anonymous'. ---> System.Net.WebException. Error en el servidor remoto: (403) Prohibido.

Paso 1: Instalar el certificado del trabajo de escalabilidad horizontal para el almacén de certificados raíz de la máquina local en el nodo del patrón de escalabilidad horizontal si todavía no está instalado y reiniciar el servicio del trabajo de escalabilidad horizontal.

Paso 2: Limpiar certificados obsoletos del almacén de certificados raíz de la máquina local en el nodo del patrón de escalabilidad horizontal.

Paso 3: Configurar SChannel para que deje de enviar la lista de entidades de certificación raíz de confianza durante el proceso del protocolo de enlace TLS/SSL mediante la edición de la entrada del Registro siguiente en el nodo del patrón de escalabilidad horizontal.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Nombre del valor: SendTrustedIssuerList 

Tipo de valor: REG_DWORD 

Datos del valor: 0 (False)

**Caso**

System.ServiceModel.CommunicationException: Error al realizar la solicitud HTTP a https://*[Nombre de la máquina]:[Puerto]*/ClusterManagement/. Este error puede deberse a que el certificado del servidor no está configurado correctamente con HTTP.SYS en la instrucción 'case' HTTPS. La causa puede ser también una falta de coincidencia del enlace de seguridad entre el cliente y el servidor. 

Paso 1: Comprobar si el certificado del patrón de escalabilidad horizontal está enlazado al puerto en el punto de conexión principal correctamente en el nodo principal con el siguiente comando. Compruebe si el hash del certificado que se muestra coincide con la huella digital del certificado del patrón de escalabilidad horizontal.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Si el enlace no es correcto, restablézcalo con los siguientes comandos y reinicie el servicio del trabajo de escalabilidad horizontal.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Síntomas**
Se produjo un error de validación al conectar el trabajo de escalabilidad horizontal al patrón de escalabilidad horizontal en el Administrador de escalabilidad horizontal. Mensaje de error: "No se puede abrir el almacén de certificados en la máquina".

### <a name="solution"></a>**Solución**

Paso 1: Ejecutar el Administrador de escalabilidad horizontal como administrador. Si lo abre con SSMS, debe ejecutar SSMS como administrador.

Paso 2: Iniciar el servicio de Registro remoto en la máquina si no se está ejecutando.

### <a name="symptoms"></a>**Síntomas**
No se inicia la ejecución en la escalabilidad horizontal.

### <a name="solution"></a>**Solución**

Compruebe el estado de las máquinas seleccionadas para ejecutar el paquete en [SSISDB].[catalog].[worker_agents]. Debe haber un trabajo en línea y habilitado como mínimo.

### <a name="symptoms"></a>**Síntomas** 
Los paquetes se ejecutan correctamente, pero no hay ningún mensaje registrado.

### <a name="solution"></a>**Solución**

Compruebe si se permite que el servidor de SQL Server que hospeda SSISDB realice la autenticación de SQL Server.

> [!Note]  
> Si cambió la cuenta para el registro de escalabilidad horizontal, consulte [Change the Account for Scale Out Logging](change-logdb-account.md) (Cambiar la cuenta para el registro de escalabilidad horizontal) y compruebe la cadena de conexión usada para el registro.

### <a name="symptoms"></a>**Síntomas**
Los mensajes de error del informe de ejecución del paquete no son suficientes para resolver los problemas.

### <a name="solution"></a>**Solución**
Puede encontrar más registros de ejecución en la carpeta TasksRootFolder configurada en WorkerSettings.config. De forma predeterminada, es \<unidad\>:\Usuarios\\*[cuenta]*\AppData\Local\SSIS\ScaleOut\Tasks. *[cuenta]* es la cuenta que ejecuta el servicio de trabajo de escalabilidad horizontal con el valor predeterminado SSISScaleOutWorker140.

Para localizar el registro de la ejecución del paquete con *[id. de ejecución]*, ejecute el comando T-SQL siguiente para obtener el *[id. de tarea]*. A continuación, busque la subcarpeta denominada *[id. de tarea]* en TasksRootFolder.<sup>1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> Esta consulta está destinada solo a solucionar problemas y está abierta a cambios si el escenario de registro y diagnóstico del trabajo de escalabilidad horizontal mejora en el futuro. 
