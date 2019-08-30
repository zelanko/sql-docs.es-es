---
title: Adaptador para la nube para SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Cloud adapter
- Deploy to Azure
ms.assetid: 82ed0d0f-952d-4d49-aa36-3855a3ca9877
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4c4e690d13f8cd12992c2b26db8e5d640a971712
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154391"
---
# <a name="cloud-adapter-for-sql-server"></a>Adaptador para la nube de SQL Server
  El servicio adaptador para la nube se crea como parte del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aprovisionamiento en una máquina virtual de Azure. El servicio Adaptador para la nube genera un certificado SSL autofirmado la primera vez que se ejecuta y, después, se ejecuta como una cuenta de **sistema local** . Genera un archivo de configuración que utiliza para configurarse a sí mismo. El adaptador para la nube también crea una regla de Firewall de Windows para permitir conexiones entrantes de TCP en el puerto predeterminado 11435.  
  
 El adaptador para la nube es un servicio sincrónico sin estado que recibe mensajes de la instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Cuando se detiene el servicio del adaptador para la nube, detiene el adaptador para la nube de acceso remoto, desenlaza el certificado SSL y deshabilita la regla de Firewall de Windows.  
  
## <a name="cloud-adapter-requirements"></a>Requisitos del adaptador para la nube  
 Tenga en cuenta los siguientes requisitos a la hora de instalar, habilitar y ejecutar el adaptador para la nube de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   El adaptador para la nube es compatible con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012 y versiones posteriores. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012, el adaptador para la nube de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requiere Objetos de administración de SQL para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2012.  
  
-   El servicio web del adaptador para la nube se ejecuta como una cuenta **Sistema local** y comprueba las credenciales del cliente antes de ejecutar cualquier tarea. Las credenciales proporcionadas por el cliente deben pertenecer a la cuenta de uso que sea miembro del grupo local de **administradores** en el equipo remoto.  
  
-   El adaptador para la nube solo admite la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   El adaptador para la nube utiliza la cuenta de administrador local de VM para ejecutar comandos en el equipo local, no una cuenta sa.  
  
-   El adaptador para la nube escucha en TCP/IP. El puerto predeterminado es 11435.  
  
-   El adaptador para la nube debe tener permisos para crear y modificar reglas de Firewall de Windows.  
  
## <a name="cloud-adapter-configuration-settings"></a>Valores de configuración del adaptador para la nube  
 Utilice los detalles de configuración siguientes para modificar la configuración de un adaptador para la nube.  
  
-   **Ruta de acceso predeterminada del archivo de configuración** : C:\Archivos de Programa\microsoft SQL Server\120\Tools\CloudAdapter\  
  
-   **Parámetros del archivo de configuración** -  
  
    -   \<configuration>  
  
        -   \<appSettings>  
  
            -   \<Add key = "WebServicePort" Value = ""/>  
  
            -   \<Add key = "WebServiceCertificate" Value = "GUID"/>  
  
            -   \<Add key = "ExposeExceptionDetails" Value = "true"/>  
  
        -   \</appSettings>  
  
    -   \</configuration>  
  
-   **Detalles del certificado** : el certificado tiene los siguientes valores:  
  
    -   Asunto: "CN = CloudAdapter\<VMName >, DC = SQL Server, DC = Microsoft"  
  
    -   El certificado solo debe tener un EKU de autenticación de servidor habilitado.  
  
    -   La longitud de la clave del certificado es 2048.  
  
 **Valores del archivo de configuración**:  
  
|Parámetro|Valores|Default|Comentarios|  
|-------------|------------|-------------|--------------|  
|WebServicePort|1-65535|11435|Cuando no se especifique, se utilizará 11435.|  
|WebServiceCertificate|Thumbprint|Empty|Si está vacío, se genera un nuevo certificado autofirmado.|  
|ExposeExceptionDetails|True/False|False||  
  
## <a name="cloud-adapter-troubleshooting"></a>Solución de problemas del adaptador para la nube  
 Use la información siguiente para solucionar problemas del adaptador para la nube de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   **Control de errores y registro** : los errores y los mensajes de estado se escriben en el registro de eventos de la aplicación.  
  
-   **Seguimiento, eventos** : todos los eventos se escriben en el registro de eventos de la aplicación.  
  
-   **Control, configuración** : Use el archivo de configuración ubicado en:  C:\Archivos de Programa\microsoft SQL\\Server\120\Tools\CloudAdapter.  
  
|Error|Id. de error|Causa|Resolución|  
|-----------|--------------|-----------|----------------|  
|Excepción al agregar el certificado al almacén de certificados. {Texto de la excepción}.|45560|Permisos del almacén de certificados de la máquina|Asegúrese de que el servicio del adaptador para la nube tenga permisos para agregar certificados al almacén de certificados del equipo.|  
|Excepción al intentar configurar el enlace SSL para el puerto {número de puerto} y el certificado {huella digital}. {Excepción}.|45561|Otra aplicación ya ha utilizado el puerto o enlazó un certificado a él.|Quite los enlaces existentes o cambie el puerto del adaptador para la nube en el archivo de configuración.|  
|No se encontró el certificado SSL [{huella digital}] en el almacén de certificados.|45564|La huella digital del certificado está en el archivo de configuración, pero el almacén de certificados personal para el servicio no contiene el certificado.<br /><br /> Permisos insuficientes.|Asegúrese de que el certificado está en el almacén de certificados personal para el servicio.<br /><br /> Asegúrese de que el servicio tiene los permisos correctos para el almacén.|  
|No se pudo iniciar el servicio web. {Texto de la excepción}.|45570|Descrito en la excepción.|Habilite ExposeExceptionDetails y utilice la información ampliada de la excepción.|  
|El certificado [{huella digital}] ha expirado.|45565|El archivo de configuración hace referencia a un certificado expirado.|Agregue un certificado válido y actualice el archivo de configuración con su huella digital.|  
|Error del servicio Web {0}:.|45571|Descrito en la excepción.|Habilite ExposeExceptionDetails y utilice la información ampliada de la excepción.|  
  
## <a name="see-also"></a>Vea también  
 [Implementar una base de datos de SQL Server en una máquina virtual de Microsoft Azure](../relational-databases/databases/deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine.md)  
  
  
