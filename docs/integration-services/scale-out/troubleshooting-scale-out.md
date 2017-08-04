---
title: "Solución de problemas de SQL Server Integration Services (SSIS) escalada | Documentos de Microsoft"
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
ms.openlocfilehash: 41bb853dd08591596f6f5baa918e174d0c26a6b5
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="troubleshooting-scale-out"></a>Solución de problemas de escalado horizontal

SSIS horizontalmente implica communtication entre SSISDB, servicios de escala Out Master y escala Out trabajo. A veces, la comunicación se interrumpe debido a errores en la configuración, la falta de permisos de acceso y otras razones. Este documento le ayudará a solucionar problemas de la configuración horizontalmente.

Para investigar los síntomas que se produce este problema, siga los pasos siguientes uno por uno hasta que se resuelva el problema.

### <a name="symptoms"></a>**Síntomas** 
Escala Out maestra no se puede conectar a SSISDB. 

Propiedades principales no se muestran en el administrador fuera de la escala.

Propiedades principales no se han rellenado [SSISDB]. [catalog]. [master_properties]

### <a name="solution"></a>**Solución**
Paso 1: Comprobar si está habilitada la opción horizontalmente.

Haga clic en **SSISDB** nodo en el Explorador de objetos de SSMS y activar **está habilitada la característica horizontalmente**.

![Está horizontalmente habilitada](media\isenabled.PNG)

Si el valor de propiedad es False, habilitar horizontalmente mediante una llamada a procedimiento almacenado [SSISDB]. [catalog]. [enable_scaleout].

Paso 2: Comprobar si el nombre de Sql Server especificado en el archivo de configuración de escala Out Master es correcta y reinicie el servicio de escala Out Master.

### <a name="symptoms"></a>**Síntomas** 
Escala Out trabajo no se puede conectar al maestro de salida de escala

No mostrar escala Out trabajo después de agregarlo en el administrador fuera de la escala

Escala Out trabajo no se muestra en [SSISDB]. [catalog]. [worker_agents]

Servicio de escala Out trabajo se está ejecutando, mientras escala Out trabajador está sin conexión

### <a name="solutions"></a>**Soluciones** 
Compruebe los mensajes de error de registro de servicio de escala Out trabajo en \<controlador\>: \Users\\*[cuenta que ejecuta el servicio de trabajo]*\AppData\Local\SSIS\Cluster\Agent.

**Caso** 

System.ServiceModel.EndpointNotFoundException: No había ningún extremo escuchando en https://*[NombreDeEquipo]: [puerto]*/ClusterManagement/ que pudiera aceptar el mensaje.

Paso 1: Compruebe si el número de puerto especificado en el archivo de configuración de servicio de escala Out maestro sea correcto y reinicie el servicio de escala Out Master. 

Paso 2: Compruebe si el punto de conexión principal especificado en la configuración de servicio de escala Out trabajo sea correcto y reinicie el servicio de escala Out trabajo.

Paso 3: Comprobar si el puerto de firewall está abierto en el nodo de escala Out Master.

Paso 4: Resolver otros problemas de conexión entre el nodo de escala Out maestra y el nodo de escala Out trabajo.

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: No puede establecer una relación de confianza para el canal seguro SSL/TLS con la entidad '*[nombre máquina]: [puerto]*'. ---> System.Net.WebException: se cerró la conexión subyacente: no se pudo establecer la relación de confianza para el canal seguro SSL/TLS. ---> System.Security.Authentication.AuthenticationException: el certificado remoto no es válido de acuerdo con el procedimiento de validación.

Paso 1: Certificado al almacén de certificados raíz del equipo local en el nodo de escala Out trabajo escala Out maestro de instalación si no aún instalado y se reinicie el servicio de escala Out trabajo.

Paso 2: Comprobar si el nombre de host en el extremo principal se incluye en el certificado de CNs de escala Out principal. Si no es así, restablecer el punto de conexión principal en el archivo de configuración de escala Out trabajo y reinicie el servicio de escala Out trabajo. 

> [!Note]
> Si no es posible cambiar el nombre de host del extremo principal debido a la configuración de DNS, tendrá que cambiar el certificado de escala Out Master. Vea [ocuparse de certificados en SSIS horizontalmente](deal-with-certificates-in-ssis-scale-out.md).

Paso 3: Comprobar si la huella digital maestra especificada en la configuración de escala Out trabajo coincide con la huella digital del certificado de escala Out Master. 

**Caso**

System.ServiceModel.Security.SecurityNegotiationException: No pudo establecer el canal seguro para SSL/TLS con la entidad '*[nombre máquina]: [puerto]*'. ---> System.Net.WebException: se anuló la solicitud: no se pudo crear el canal seguro SSL/TLS.

Paso 1: Comprobar si la cuenta que ejecuta el servicio escala Out Worker tiene acceso al certificado de escala Out trabajo mediante el siguiente comando.

```dos
winhttpcertcfg.exe -l -c LOCAL_MACHINE\MY -s {CN of the worker certificate}
```

Si la cuenta no tiene acceso, concede mediante el comando siguiente y reinicie el servicio de escala Out trabajo.

```dos
winhttpcertcfg.exe -g -c LOCAL_MACHINE\My -s {CN of the worker certificate} -a {the account running Scale Out Worker service}
```

**Caso**

System.ServiceModel.Security.MessageSecurityException: Se prohíbe la solicitud HTTP con el esquema de autenticación de cliente 'Anonymous'. ---> System.Net.WebException: el servidor remoto devolvió un error: (403) prohibido.

Paso 1: Certificado al almacén de certificados raíz del equipo local en el nodo de escala Out Master instalación escala Out trabajo si no aún instalado y se reinicie el servicio de escala Out trabajo.

Paso 2: Limpiar inútiles certificados en el almacén de certificados raíz del equipo local en el nodo de escala Out Master.

Paso 3: Configurar Schannel para no volverá a enviar la lista de entidades de certificación raíz de confianza durante el proceso de negociación TLS/SSL, mediante la adición de la entrada del registro siguiente en el nodo de escala Out Master.

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Nombre del valor: SendTrustedIssuerList 

Tipo de valor: REG_DWORD 

Datos del valor: 0 (False)

**Caso**

System.ServiceModel.CommunicationException: Se produjo un error al realizar la solicitud HTTP a https://*[nombre máquina]: [puerto]*  /ClusterManagement /. Esto puede deberse al hecho de que el certificado de servidor no está configurado correctamente con HTTP. SYS en el caso HTTPS. Esto también podría deberse a un error de coincidencia del enlace de seguridad entre el cliente y el servidor. 

Paso 1: Comprobar si escala Out Master certificado está enlazado al puerto en el punto de conexión principal correctamente en el nodo principal con el siguiente comando. Compruebe si el hash del certificado muestra coincide con la huella digital de certificado de escala Out Master.

```dos
netsh http show sslcert ipport=0.0.0.0:{Master port}
```

Si el enlace no es correcto, restablézcala con los siguientes comandos y reinicie el servicio de escala Out trabajo.

```dos
netsh http delete sslcert ipport=0.0.0.0:{Master port}
netsh http add sslcert ipport=0.0.0.0:{Master port} certhash={Master certificate thumbprint} certstorename=Root appid={random guid}
```

### <a name="symptoms"></a>**Síntomas**
No iniciar la ejecución en horizontalmente.

### <a name="solution"></a>**Solución**

Compruebe el estado de los equipos seleccionados para ejecutar el paquete en [SSISDB]. [catalog]. [worker_agents]. Al menos un trabajo debe estar conectado y habilitado.

### <a name="symptoms"></a>**Síntomas** 
Paquetes funcionan correctamente, pero no hay ningún mensaje registrado.

### <a name="solution"></a>**Solución**

Compruebe si se permite la autenticación de SQL Server por el servidor Sql Server que se hospeda SSISDB.

> [!Note]  
> Si ha cambiado la cuenta para el registro horizontalmente, consulte [cambiar la cuenta para la escala fuera registro](change-logdb-account.md) y compruebe la cadena de conexión que se usa para el registro.

### <a name="symptoms"></a>**Síntomas**
Los mensajes de error en el informe de ejecución del paquete no son suficientes para solucionar el problema.

### <a name="solution"></a>**Solución**
Número de registros de ejecución puede encontrarse en TasksRootFolder configurado en WorkerSettings.config. De forma predeterminada, es \<controlador\>: \Users\\*[account]*\AppData\Local\SSIS\ScaleOut\Tasks. El *[account]* es la cuenta que ejecuta el servicio escala Out Worker con el valor predeterminado SSISScaleOutWorker140.

Para buscar el registro para la ejecución del paquete con *[Id. de ejecución]*, ejecute el comando de T-SQL siguiente para obtener la *[Id. de tarea]*. A continuación, busque la subcarpeta denominada con *[Id. de tarea]* en TasksRootFolder.<sup> 1<sup>

```sql
SELECT [TaskId]
FROM [SSISDB].[internal].[tasks] tasks, [SSISDB].[internal].[executions] executions 
WHERE executions.execution_id = *Your Execution Id* AND tasks.JobId = executions.job_id
```
<sup>1</sup> esta consulta es para solucionar problemas de propósito único y abra cambiar cuando el escenario de registro y diagnóstico para escala Out trabajador se ha mejorado en el futuro. 
