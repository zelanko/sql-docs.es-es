---
title: "Instalación de PolyBase | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PolyBase, installation
ms.assetid: 3a1e64be-9bfc-4408-accd-35990e1a6b52
caps.latest.revision: 25
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 6aa73e749d4f308265dfe27a160802c15a391a3e
ms.openlocfilehash: 9a4f230e8c25a24f85f36f3a1aaf82fbf247cd9a
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="polybase-installation"></a>Instalación de PolyBase
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para instalar una versión de prueba de SQL Server, vaya a [SQL Server Evaluaciones](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016). 
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Edición de evaluación de SQL Server (64 bits).  
  
-   Microsoft .NET Framework 4.5.  
  
-   La versión de Oracle Java SE RunTime Environment (JRE) 7.51 o una superior (64 bits) ( [JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) o [Server JRE](http://www.oracle.com/technetwork/java/javase/downloads/server-jre8-downloads-2133154.html) funcionará). Vaya a la página de [descargas de Java SE](http://www.oracle.com/technetwork/java/javase/downloads/index.html). El programa de instalación generará un error si JRE no está presente.  
  
-   Memoria mínima: 4 GB.  
  
-   Espacio disponible en disco duro mínimo: 2 GB.  
  
-   TCP/IP debe estar habilitado para que Polybase funcione correctamente. TCP/IP está habilitado de manera predeterminada en todas las ediciones de SQL Server, excepto en las ediciones Developer y Express de SQL Server. Para que Polybase funcione correctamente en las ediciones Developer y Express debe habilitar la conectividad TCP/IP (consulte [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)).
  
 **Notas**  
  
 PolyBase solo se puede instalar en una instancia de SQL Server por máquina.  
  
## <a name="single-node-or-polybase-scaleout-group"></a>Nodo único o grupo de escalado horizontal de PolyBase
Antes de iniciar la instalación de PolyBase en las instancias de SQL Server, recomendamos decidir si desea una instalación de nodo único o un grupo de escalado horizontal de PolyBase. Para un grupo de escalado horizontal de PolyBase, debe asegurarse de lo siguiente: 
- Todas las máquinas están en el mismo dominio.
- Utilice la misma cuenta y contraseña de servicio durante la instalación.
- Que las instancias de SQL Server pueden comunicarse entre sí a través de la red.

Una vez haya instalado PolyBase como un grupo de escalado horizontal o de forma independiente, no podrá cambiarlo. Tendrá que desinstalar y volver a instalar la característica para cambiar esta configuración.

## <a name="install-using-the-installation-wizard"></a>Instalación con el Asistente para instalación  
  
1.  Ejecute **Centro de instalación de SQL Server**. Inserte el medio de instalación de SQL Server y haga doble clic en **Setup.exe**.  
  
2.  Haga clic en **Instalación**y, después, en **New Standalone SQL Server installation or add features**(Nueva instalación independiente de SQL Server o adición de características).  
  
3.  En la página Selección de características, elija **PolyBase Query Service for External Data**(Servicio de consultas PolyBase para datos externos).  
  
4.  En la página Configuración del servidor, configure el **servicio de motor de SQL Server PolyBase** y el servicio de movimiento de datos de SQL Server PolyBase para que se ejecuten en la misma cuenta.  
  
    > **IMPORTANTE:** En un grupo de escalado horizontal de PolyBase, el servicio de movimiento de datos de PolyBase y el motor de PolyBase de todos los nodos debe ejecutarse en la misma cuenta de dominio.  
    > Consulte Scaling out PolyBase (Escalado horizontal de PolyBase).  
  
5.  En la página **PolyBase Configuration**(Configuración de PolyBase), seleccione una de las dos opciones. Consulte [PolyBase scale-out groups (Grupos de escalado horizontal de PolyBase)](../../relational-databases/polybase/polybase-scale-out-groups.md) para obtener más información.  
  
    -   Use la instancia de SQL Server como una instancia independiente habilitada para PolyBase.  
  
         Elija esta opción para usar la instancia de SQL Server como un nodo principal independiente.  
  
    -   Utilice la instancia de SQL Server como parte de un grupo de escalado horizontal de PolyBase.  Si selecciona esta opción, se abrirá el firewall para permitir las conexiones entrantes al motor de base de datos de SQL Server, al motor de SQL Server PolyBase, al servicio de movimiento de datos de SQL Server PolyBase y a SQL Browser. Se abrirá el firewall para permitir las conexiones entrantes desde otros nodos de un grupo de escalado horizontal de PolyBase.  
  
         Al seleccionar esta opción, también se habilitarán las conexiones de firewall de Microsoft DTC (Coordinador de transacciones distribuidas) y se modificará la configuración del registro de Microsoft DTC.  
  
6.  En la página **PolyBase Configuration**(Configuración de PolyBase), especifique un intervalo de puertos con al menos seis puertos. El programa de instalación de SQL Server asignará los seis primeros puertos disponibles del intervalo.  
  
##  <a name="installing"></a> Instalación mediante un símbolo del sistema  
 Use los valores de esta tabla para crear scripts de instalación. Los dos servicios, el de **motor de SQL Server PolyBase** y el de **movimiento de datos de SQL Server PolyBase** , deben ejecutarse en la misma cuenta. En un grupo de escalado horizontal de PolyBase, se deben ejecutar con la misma cuenta de dominio los servicios de PolyBase en todos los nodos.  
  
|Componente de SQL Server|Parámetro y valores|Descripción|  
|--------------------------|--------------------------|-----------------|  
|Control del programa de instalación de SQL Server|**Necesario**<br /><br /> /FEATURES=PolyBase|Selecciona la característica PolyBase.|  
|motor de SQL Server PolyBase|**Opcional**<br /><br /> /PBENGSVCACCOUNT|Especifica la cuenta del servicio de motor. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|motor de SQL Server PolyBase|**Opcional**<br /><br /> /PBENGSVCPASSWORD|Especifica la contraseña de la cuenta del servicio de motor.|  
|motor de SQL Server PolyBase|**Opcional**<br /><br /> /PBENGSVCSTARTUPTYPE|Especifica el modo de inicio para el servicio de motor de PolyBase: Automático (predeterminado), Deshabilitado y Manual.|  
|movimiento de datos de SQL Server PolyBase|**Opcional**<br /><br /> /PBDMSSVCACCOUNT|Especifica la cuenta del servicio de movimiento de datos. El valor predeterminado es **NT Authority\NETWORK SERVICE**.|  
|movimiento de datos de SQL Server PolyBase|**Opcional**<br /><br /> /PBDMSSVCPASSWORD|Especifica la contraseña de la cuenta de movimiento de datos.|  
|movimiento de datos de SQL Server PolyBase|**Opcional**<br /><br /> /PBDMSSVCSTARTUPTYPE|Especifica el modo de inicio para el servicio de movimiento de datos: Automático (predeterminado), Deshabilitado y Manual.|  
|PolyBase|**Opcional**<br /><br /> /PBSCALEOUT|Especifica si la instancia de SQL Server se utilizará como parte del grupo de cálculo de escalabilidad horizontal de PolyBase. <br />Valores admitidos: **True**, **False**.|  
|PolyBase|**Opcional**<br /><br /> /PBPORTRANGE|Especifica un intervalo de puertos con un mínimo de 6 puertos para los servicios de PolyBase. Ejemplo:<br /><br /> `/PBPORTRANGE=16450-16460`|  
  
 **Ejemplo**  
  
 Muestra un script de instalación de ejemplo.  
  
```  
  
Setup.exe /Q /ACTION=INSTALL /IACCEPTSQLSERVERLICENSETERMS /FEATURES=SQLEngine,Polybase   
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="\<fabric-domain>\Administrator"   
/INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /PBSCALEOUT=TRUE   
/PBPORTRANGE=16450-16460 /SECURITYMODE=SQL /SAPWD="<StrongPassword>"   
/PBENGSVCACCOUNT="<DomainName>\<UserName>" /PBENGSVCPASSWORD="<StrongPassword>"   
/PBDMSSVCACCOUNT="<DomainName>\<UserName>" /PBDMSSVCPASSWORD="<StrongPassword>"  
  
```  
  
## <a name="post-installation-notes"></a>Notas posteriores a la instalación  
 PolyBase instala tres bases de datos de usuario: DWConfiguration, DWDiagnostics y DWQueue.   Son para uso de PolyBase y no se deben modificar ni eliminar.  
  
### <a name="how-to-confirm-installation"></a>Cómo confirmar la instalación  
 Ejecute el siguiente comando: Si PolyBase está instalado, devuelve 1; en caso contrario, 0.  
  
```tsql  
SELECT SERVERPROPERTY ('IsPolybaseInstalled') AS IsPolybaseInstalled;  
```  
  
### <a name="firewall-rules"></a>Reglas de firewall  
 El programa de instalación de SQL Server PolyBase crea las siguientes reglas de firewall en la máquina.  
  
-   SQL Server PolyBase - Motor de base de datos - \<nombreDeInstanciaDeSQLServer> (TCP de entrada)  
  
-   SQL Server PolyBase -> Servicios de PolyBase - \<nombreDeInstanciaDeSQLServer> (TCP de entrada)  
  
-   SQL Server PolyBase -> SQL Browser -> (UDP de entrada)  
  
 Durante la instalación, si decide usar la instancia de SQL Server como parte de un grupo de escalabilidad horizontal de PolyBase, estas reglas se habilitan y se abre el firewall para permitir conexiones entrantes al motor de base de datos de SQL Server, al motor de SQL Server PolyBase, al servicio de movimiento de datos de SQL Server PolyBase y a SQL Browser. Sin embargo, si no se está ejecutando el servicio del firewall en la máquina durante la instalación, el programa de instalación de SQL Server no podrá habilitar estas reglas. En ese caso, debe iniciar el servicio del firewall en la máquina y habilitar reglas después de la instalación.  
  
#### <a name="to-enable-the-firewall-rules"></a>Para habilitar las reglas de firewall, siga estos pasos:  
  
-   Abra el **Panel de control**.  
  
-   Haga clic en **Sistema y seguridad**y, después, en **Firewall de Windows**.  
  
-   Haga clic en **Configuración avanzada**y, después, en **Reglas de entrada**.  
  
-   Haga clic con el botón derecho en la regla deshabilitada y, luego, haga clic en **Habilitar regla**.  
  
### <a name="polybase-service-accounts"></a>Cuentas de servicio de PolyBase
Para cambiar las cuentas de servicio del motor de PolyBase y de los servicios de movimiento de datos de PolyBase, desinstale y vuelva a instalar la característica PolyBase.
   
## <a name="next-steps"></a>Pasos siguientes  
 Consulte [PolyBase configuration](../../relational-databases/polybase/polybase-configuration.md).  
  
  

