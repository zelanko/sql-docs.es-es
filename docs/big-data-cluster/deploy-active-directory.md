---
title: Implementación en el modo de Active Directory
titleSuffix: SQL Server Big Data Cluster
description: Obtenga información sobre cómo actualizar los clústeres de macrodatos de SQL Server en un dominio Active Directory.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 02/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 2bbacb2bdeeb409f08e6e68438535bc0d6671b01
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "79487623"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode"></a>Implementación de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en el modo de Active Directory

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este documento se describe la implementación de un clúster de macrodatos SQL Server 2019 (BDC) en el modo de autenticación de Active Directory, el cual usará un dominio de AD existente para la autenticación.

## <a name="background"></a>Información previa

Para habilitar la autenticación Active Directory (AD), el BDC crea automáticamente los usuarios, los grupos, las cuentas de máquina y los nombres de entidad de seguridad de servicio (SPN) que necesitan los distintos servicios del clúster. Para proporcionar cierta independencia respecto de estas cuentas y posibilitar el uso de permisos de ámbito, designe una unidad organizativa (UO) durante la implementación, donde se crearán todos los objetos de AD relacionados con el BDC. Cree esta UO antes de la implementación del clúster.

Para crear automáticamente todos los objetos necesarios en Active Directory, el BDC necesita una cuenta de AD durante la implementación. Esta cuenta debe tener permisos para crear usuarios, grupos y cuentas de máquina dentro de la UO proporcionada.

En los pasos siguientes se da por hecho que ya cuenta con un controlador de dominio de Active Directory. Si no se tiene un controlador de dominio, la [guía](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) siguiente incluye pasos que pueden resultar útiles.

## <a name="create-ad-objects"></a>Creación de objetos de AD

Antes de implementar un BDC con la integración de AD, haga lo siguiente:

1. Cree una unidad organizativa (UO) donde se almacenarán todos los objetos de AD del BDC. También puede optar por designar una UO existente durante la implementación.
1. Cree una cuenta de AD para el BDC o use una cuenta existente y proporcione los permisos adecuados a esta cuenta de AD del BDC.

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Creación de un usuario en AD para la cuenta de servicio de dominio del BDC

El clúster de macrodatos requiere una cuenta con permisos específicos. Antes de continuar, asegúrese de tener una cuenta de AD existente o cree una nueva cuenta, que puede usar el clúster de macrodatos para configurar los objetos necesarios.

Para crear un nuevo usuario en AD, puede hacer clic con el botón derecho en el dominio o la UO y seleccionar **Nuevo** > **Usuario**:

![image12](./media/deploy-active-directory/image12.png)

En este artículo se hará referencia a este usuario como la *cuenta de servicio de dominio del BDC*.

### <a name="creating-an-ou"></a>Creación de una unidad organizativa

En el controlador de dominio, abra **Usuarios y equipos de Active Directory**. En el panel izquierdo, haga clic con el botón derecho en el directorio en el que quiera crear la UO y seleccione Nuevo \>**Unidad organizativa** y, después, siga las indicaciones del asistente para crearla. También puede crear una UO con PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

En los ejemplos de este artículo, vamos a asignar el nombre `bdc` a la UO.

![image13](./media/deploy-active-directory/image13.png)

![image14](./media/deploy-active-directory/image14.png)

### <a name="setting-permissions-the-bdc-ad-account"></a>Establecimiento de permisos para la cuenta de AD del BDC

Tanto si se ha creado un nuevo usuario de AD como si se usa uno existente, existen ciertos permisos que el usuario debe tener. Esta cuenta es la cuenta de usuario que el controlador del BDC usará al unir el clúster a AD.

La cuenta de servicio de dominio (DSA) del BDC debe ser capaz de crear usuarios, grupos y cuentas de equipo en la UO. En los pasos siguientes, el nombre que hemos asignado a la cuenta de servicio de dominio del BDC es `bdcDSA`. Se puede elegir cualquier nombre para esta cuenta.

1. En el controlador de dominio, abra **Usuarios y equipos de Active Directory**.

1. En el panel izquierdo, navegue hasta el dominio y, luego, hasta la UO que usará `bdc`.

1. Haga clic con el botón derecho en la UO y seleccione **Propiedades**.

1. Asegúrese de haber seleccionado **Características avanzadas** haciendo clic con el botón derecho en la UO y seleccionando **Ver**, y vaya a la pestaña Seguridad.

    ![image15](./media/deploy-active-directory/image15.png)

1. Haga clic en **Agregar...** y agregue el usuario **bdcDSA**.

    ![image16](./media/deploy-active-directory/image16.png)

    ![image17](./media/deploy-active-directory/image17.png)

1. Seleccione el usuario **bdcDSA**, borre todos los permisos y haga clic en **Avanzado**.

1. Haga clic en **Agregar**.

    ![image18](./media/deploy-active-directory/image18.png)

    - Haga clic en **Seleccionar una entidad de seguridad**, inserte **bdcDSA** y haga clic en Aceptar.

    - Establezca **Tipo** en **Permitir**.

    - Establezca **Se aplica a** en **Este objeto y todos los descendientes**.

        ![image19](./media/deploy-active-directory/image19.png)

    - Desplácese hasta la parte inferior y haga clic en **Borrar todo**.

    - Desplácese hacia la parte superior y seleccione lo siguiente:
       - **Leer todas las propiedades**
       - **Escribir todas las propiedades**
       - **Crear objetos de equipo**
       - **Eliminar objetos de equipo**
       - **Crear objetos de grupo**
       - **Eliminar objetos de grupo**
       - **Crear objetos de usuario**
       - **Eliminación de objetos de usuario**

    - Haga clic en **Aceptar**

- Haga clic en **Agregar**.

    - Haga clic en **Seleccionar una entidad de seguridad**, inserte **bdcDSA** y haga clic en Aceptar.

    - Establezca **Tipo** en **Permitir**.

    - Establezca **Se aplica a** en **Objetos de equipo descendientes**.

    - Desplácese hasta la parte inferior y haga clic en **Borrar todo**.

    - Desplácese hacia la parte superior y seleccione **Restablecer contraseña**.

    - Haga clic en **Aceptar**

- Haga clic en **Agregar**.

    - Haga clic en **Seleccionar una entidad de seguridad**, inserte **bdcDSA** y haga clic en Aceptar.

    - Establezca **Tipo** en **Permitir**.

    - Establezca **Se aplica a** en **Objetos de usuario descendientes**.

    - Desplácese hasta la parte inferior y haga clic en **Borrar todo**.

    - Desplácese hacia la parte superior y seleccione **Restablecer contraseña**.

    - Haga clic en **Aceptar**

- Haga clic en **Aceptar** dos veces más para cerrar los cuadros de diálogo abiertos.

## <a name="prepare-deployment"></a>Preparación de la implementación

Para la implementación del BDC con la integración de AD, hay cierta información adicional que se debe proporcionar para la creación de los objetos relacionados con el BDC en AD.

Con el uso del perfil `kubeadm-prod`, tendrá automáticamente los marcadores de posición para la información relacionada con la seguridad y con el punto de conexión que se necesitan para la integración de AD.

Además, debe proporcionar las credenciales que [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] usará para crear los objetos necesarios en AD. Estas credenciales se proporcionan como variables de entorno.

## <a name="set-security-environment-variables"></a>Establecimiento de variables de entorno de seguridad

Las siguientes variables de entorno proporcionan las credenciales para la cuenta de servicio de dominio del BDC, que se usarán para configurar la integración de AD. El BDC también usa esta cuenta para mantener en el futuro los objetos de AD relacionados con el BDC.

```bash
export DOMAIN_SERVICE_ACCOUNT_USERNAME=<AD principal account name>
export DOMAIN_SERVICE_ACCOUNT_PASSWORD=<AD principal password>
```

## <a name="provide-security-and-endpoint-parameters"></a>Suministro de seguridad y parámetros de punto de conexión

Además de las variables de entorno para las credenciales, también debe proporcionar información de seguridad y de punto de conexión para que la integración de AD funcione. Los parámetros necesarios forman parte automáticamente del [perfil de implementación](deployment-guidance.md#configfile) de `kubeadm-prod`.

La integración de AD necesita los parámetros siguientes. Agregue estos parámetros a los archivos `control.json` y `bdc.json` con los comandos `config replace` que se muestran más adelante en este artículo. Todos los ejemplos siguientes utilizan `contoso.local` de dominio de ejemplo.

- `security.activeDirectory.ouDistinguishedName`: nombre distintivo de una unidad organizativa (UO) en la que se agregarán todas las cuentas de AD que cree la implementación del clúster. Si se llama al dominio `contoso.local`, el nombre distintivo de la UO será `OU=BDC,DC=contoso,DC=local`.

- `security.activeDirectory.dnsIpAddresses`: contiene la lista de direcciones IP de los servidores DNS del dominio. 

- `security.activeDirectory.domainControllerFullyQualifiedDns`: lista de FQDN del controlador de dominio. El FQDN contiene el nombre de host o de la máquina del controlador de dominio. Si tiene varios controladores de dominio, aquí se puede proporcionar una lista. Ejemplo: `HOSTNAME.CONTOSO.LOCAL`

- **Parámetro opcional** `security.activeDirectory.realm`: en la mayoría de casos, el dominio es igual al nombre de dominio. En los casos en los que no sean iguales, use este parámetro para definir el nombre del dominio (por ejemplo, `CONTOSO.LOCAL`).

- `security.activeDirectory.domainDnsName`: nombre del dominio (por ejemplo, `contoso.local`).

- `security.activeDirectory.clusterAdmins`: este parámetro toma un grupo de AD. El ámbito del grupo de AD debe ser universal o global del dominio. Los miembros de este grupo obtienen permisos de administrador en el clúster. Esto significa que tendrán permisos `sysadmin` en SQL Server, permisos de superusuario en HDFS y de administrador en el controlador. 

  >[!IMPORTANT]
  >Cree este grupo en AD antes de comenzar la implementación. Si el ámbito de este grupo de AD es el dominio local, se produce un error en la implementación.

- `security.activeDirectory.clusterUsers`: lista de los grupos de AD que son usuarios normales (sin permisos de administrador) en el clúster de macrodatos. La lista puede incluir grupos de AD cuyo ámbito sean grupos de dominio universal o global. No pueden ser grupos de dominio local.

  >[!IMPORTANT]
  >Cree estos grupos en AD antes de comenzar la implementación. Si el ámbito de cualquiera de estos grupos de AD es el dominio local, se produce un error en la implementación.

- **Parámetro opcional** `security.activeDirectory.appOwners`: lista de grupos de AD que tienen permisos para crear, eliminar y ejecutar cualquier aplicación. La lista puede incluir grupos de AD cuyo ámbito sean grupos de dominio universal o global. No pueden ser grupos de dominio local.

  >[!IMPORTANT]
  >Cree estos grupos en AD antes de comenzar la implementación. Si el ámbito de cualquiera de estos grupos de AD es el dominio local, se produce un error en la implementación.

- **Parámetro opcional** `security.activeDirectory.appReaders`: lista de grupos de AD que tienen permisos para ejecutar cualquier aplicación. La lista puede incluir grupos de AD cuyo ámbito sean grupos de dominio universal o global. No pueden ser grupos de dominio local.

  >[!IMPORTANT]
  >Cree estos grupos en AD antes de comenzar la implementación. Si el ámbito de cualquiera de estos grupos de AD es el dominio local, se produce un error en la implementación.

[Compruebe el ámbito del grupo de AD](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps), para determinar si es DomainLocal.

Si aún no ha inicializado el archivo de configuración de la implementación, puede ejecutar este comando para obtener una copia de la configuración.

```bash
azdata bdc config init --source kubeadm-prod  --target custom-prod-kubeadm
```

Para establecer los parámetros anteriores en el archivo `control.json`, use los siguientes comandos de `azdata`. Los comandos reemplazan la configuración y proporcionan sus propios valores antes de que se realice la implementación.

 > [!IMPORTANT]
 > En la versión SQL Server 2019 CU2, la estructura de la sección de configuración de seguridad del perfil de implementación ha cambiado ligeramente y todos los valores relacionados con Active Directory están en el nuevo directorio *activeDirectory* en el árbol de JSON, bajo *security*, en el archivo *control.json*.

El ejemplo siguiente se basa en el uso de SQL Server 2019 CU2. Se muestra cómo reemplazar los valores de parámetros relacionados con AD en la configuración de implementación. Los detalles del dominio siguientes son valores de ejemplo.

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.activeDirectory.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Del mismo modo, en las versiones anteriores a SQL Server 2019 CU2, puede ejecutar lo siguiente:

```bash
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.ouDistinguishedName=OU\=bdc\,DC\=contoso\,DC\=local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.dnsIpAddresses=[\"10.100.10.100\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainControllerFullyQualifiedDns=[\"HOSTNAME.CONTOSO.LOCAL\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.domainDnsName=contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterAdmins=[\"bdcadminsgroup\"]"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.security.clusterUsers=[\"bdcusersgroup\"]"
#Example for providing multiple clusterUser groups: [\"bdcusergroup1\",\"bdcusergroup2\"]
```

Además de la información anterior, también debe proporcionar nombres de DNS para los distintos puntos de conexión del clúster. Las entradas DNS que usan los nombres de DNS proporcionados se crearán automáticamente en el servidor DNS tras la implementación. Usará estos nombres al conectarse a los diferentes puntos de conexión del clúster. Por ejemplo, si el nombre de DNS de la instancia maestra de SQL es `mastersql`, usará `mastersql.contoso.local,31433` para conectarse a la instancia maestra desde las herramientas.

> [!NOTE]
> Asegúrese de crear entradas DNS en el servidor DNS para los nombres que va a definir a continuación. En el caso de las implementaciones de `kubeadm`, puede usar, por ejemplo, la dirección IP del nodo maestro de Kubernetes al crear las entradas DNS.

```bash
# DNS names for BDC services
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[0].dnsName=<controller DNS name>.contoso.local"
azdata bdc config replace -c custom-prod-kubeadm/control.json -j "$.spec.endpoints[1].dnsName=<monitoring services DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[0].dnsName=<SQL Master Primary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.master.spec.endpoints[1].dnsName=<SQL Master Secondary DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.gateway.spec.endpoints[0].dnsName=<Gateway (Knox) DNS name>.<Domain name. e.g. contoso.local>"
azdata bdc config replace -c custom-prod-kubeadm/bdc.json -j "$.spec.resources.appproxy.spec.endpoints[0].dnsName=<app proxy DNS name>.<Domain name. e.g. contoso.local>"
```

Puede encontrar un script de ejemplo aquí para la [implementación de un clúster de macrodatos de SQL Server en un clúster de Kubernetes de un solo nodo (kubeadm) con integración de AD](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm/ubuntu-single-node-vm-ad).

Ahora debe haber establecido todos los parámetros necesarios para una implementación del BDC con la integración de Active Directory.

Ahora puede implementar el clúster de BDC integrado con Active Directory mediante el comando `azdata` y el perfil de implementación kubeadm-prod. Para obtener la documentación completa sobre cómo implementar [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)], visite [Procedimiento para implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md).

## <a name="verify-reverse-dns-entry-for-domain-controller"></a>Comprobación de la entrada de DNS inverso para el controlador de dominio

Asegúrese de que haya una entrada de DNS inverso (registro PTR) para el propio controlador de dominio registrada en el servidor DNS. Puede comprobarlo ejecutando el elemento `nslookup` del nombre de dominio en el controlador de dominio para ver que se pueda resolver en la dirección IP del controlador de dominio.

## <a name="connect-to-cluster-endpoints-in-ad-mode"></a>Conexión a los puntos de conexión del clúster en el modo de AD

Inicie sesión en la instancia maestra de SQL Server con la autenticación de AD.

Para comprobar las conexiones de AD a la instancia de SQL Server, conéctese a la instancia maestra de SQL con `sqlcmd`. Los inicios de sesión para los grupos proporcionados se crean automáticamente tras la implementación (`clusterUsers` y `clusterAdmins`).

Si usa Linux, ejecute `kinit` primero como usuario de AD y, luego, `sqlcmd`. Si usa Windows, solo tiene que iniciar la sesión del usuario que prefiera desde una **máquina de cliente unida a un dominio**.

### <a name="connect-to-master-instance-from-linuxmac"></a>Conexión a una instancia maestra desde Linux/Mac

```bash
kinit <username>@<domain name>
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="connect-to-master-instance-from-windows"></a>Conexión a una instancia maestra desde Windows

```cmd
sqlcmd -S <DNS name for master instance>,31433 -E
```

### <a name="log-in-to-sql-server-master-instance-using-azure-data-studio-or-ssms"></a>Inicio de sesión en la instancia maestra de SQL Server con Azure Data Studio o SSMS

Desde un cliente unido a un dominio, se puede abrir SSMS o Azure Data Studio y conectarse a la instancia maestra. Esta es la misma experiencia que la conexión a cualquier instancia de SQL Server mediante la autenticación de AD.

Desde SSMS:

![image23](./media/deploy-active-directory/image23.png)

Desde Azure Data Studio:

![image24](./media/deploy-active-directory/image24.png)}

### <a name="log-in-to-controller-with-ad-authentication"></a>Inicio de sesión en el controlador con la autenticación de AD

#### <a name="connect-to-controller-with-ad-authentication-from-linuxmac"></a>Conexión al controlador con la autenticación de AD desde Linux/Mac

Puede conectarse al punto de conexión del controlador mediante `azdata` y la autenticación de AD.

```bash
kinit <username>@<domain name>
azdata login -e https://<controller DNS name>:30080 --auth ad
```

#### <a name="connect-to-controller-with-ad-authentication-from-windows"></a>Conexión al controlador con la autenticación de AD desde Windows

```cmd
azdata login -e https://<controller DNS name>:30080 --auth ad
```

### <a name="use-ad-authentication-to-knox-gateway-webhdfs"></a>Uso de la autenticación de AD en la puerta de enlace Knox (webHDFS)

También se pueden emitir comandos HDFS mediante el uso de curl a través del punto de conexión de la puerta de enlace Knox. Esto requiere la autenticación de AD en Knox. El siguiente comando curl emite una llamada REST de webHDFS a través de la puerta de enlace Knox para crear un directorio denominado `products`

```bash
curl -k -v --negotiate -u : https://<Gateway DNS name>:30443/gateway/default/webhdfs/v1/products?op=MKDIRS -X PUT
```

## <a name="known-issues-and-limitations"></a>Limitaciones y problemas conocidos

**Limitaciones que deben tenerse en cuenta en esta versión:**

- Actualmente, los paneles Búsqueda de registros y Métricas no admiten la autenticación de AD. La compatibilidad de AD con este punto de conexión está prevista para una versión futura. El nombre de usuario y la contraseña básicos establecidos tras la implementación se pueden usar para la autenticación en estos paneles. El resto de puntos de conexión del clúster admiten la autenticación de AD.

- Por el momento, el modo de AD seguro solo funcionará en entornos de implementación de `kubeadm`, pero no en AKS. De forma predeterminada, el perfil de implementación de `kubeadm-prod` incluye las secciones de seguridad.

- Por el momento solo se permite un BDC por dominio (Active Directory). La habilitación de varios BDC por dominio está prevista para una versión futura.

- Ninguno de los grupos de AD especificados en las configuraciones de seguridad puede tener definido el ámbito DomainLocal. Puede comprobar el ámbito de un grupo de AD siguiendo [estas instrucciones](https://docs.microsoft.com/powershell/module/activedirectory/get-adgroup?view=winserver2012-ps&viewFallbackFrom=winserver2012r2-ps).

- Se permite la cuenta de AD que se puede usar para iniciar sesión en BDC desde el mismo dominio que se ha configurado para BDC; la habilitación de inicios de sesión desde otro dominio de confianza está planeada para una versión futura.
