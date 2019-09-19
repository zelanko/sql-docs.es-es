---
title: Montaje de ADLS Gen2 para los niveles de HDFS
titleSuffix: How to mount ADLS Gen2
description: En este artículo se explica cómo configurar la organización en niveles de HDFS para montar un sistema de archivos de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]Azure Data Lake Storage externo en HDFS en un.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/27/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f209d249fb0e289258aa20bbfafd8a715dc463d6
ms.sourcegitcommit: b016c01c47bc08351d093a59448d895cc170f8c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/19/2019
ms.locfileid: "71118121"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Procedimiento para montar ADLS Gen2 para los niveles de HDFS en un clúster de macrodatos

En las secciones siguientes se proporciona un ejemplo de cómo configurar los niveles de HDFS con un origen de datos de Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de macrodatos implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a> Carga de datos en Azure Data Lake Storage

En la siguiente sección se describe cómo configurar Azure Data Lake Storage Gen2 para probar los niveles de HDFS. Si ya tiene datos almacenados en Azure Data Lake Storage, puede omitir esta sección y usar sus propios datos.

1. [Cree una cuenta de almacenamiento con capacidades de Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Cree un sistema de archivos o contenedor de blobs](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) en esta cuenta de almacenamiento para los datos externos.

1. Cargue un archivo .csv o Parquet en el contenedor. Estos son los datos de HDFS externos que se montarán en HDFS en el clúster de macrodatos.

## <a name="credentials-for-mounting"></a>Credenciales para el montaje

### <a name="use-oauth-credentials-to-mount"></a>Uso de credenciales de OAuth para el montaje

Para poder usar las credenciales de OAuth para el montaje, debe llevar a cabo los pasos siguientes:

1. Vaya a [Azure Portal](https://portal.azure.com).
1. Vaya a "Azure Active Directory". Debería ver este servicio en la barra de navegación izquierda.
1. En la barra de navegación derecha, seleccione "Registros de aplicaciones" y cree un nuevo registro.
1. Cree una aplicación web y siga el asistente. **Recuerde el nombre de la aplicación que cree aquí**. Tendrá que agregar este nombre a su cuenta de ADLS como usuario autorizado. Tenga en cuenta también el identificador de cliente de la aplicación en la información general cuando seleccione la aplicación.
1. Una vez creada la aplicación Web, vaya a "certificados & Secrets" y cree un **nuevo secreto de cliente** y seleccione una duración de clave. **Agregue** el secreto.
1.  Vuelva a la página registros de aplicaciones y haga clic en los "puntos de conexión" en la parte superior. **Anote el "punto de conexión del token de OAuth (V2)** Dirección
1. Debería tener anotado lo siguiente para OAuth:

    - "ID. de cliente de aplicación" de la aplicación Web
    - El secreto de cliente
    - El punto de conexión del token

### <a name="adding-the-service-principal-to-your-adls-account"></a>Adición de la entidad de servicio a la cuenta de ADLS

1. Vuelva al portal y vaya al sistema de archivos de la cuenta de almacenamiento de ADLS y seleccione control de acceso (IAM) en el menú de la izquierda.
1. Seleccione "agregar una asignación de roles". 
1. Seleccionar rol "colaborador de datos de BLOB de almacenamiento"
1. Busque el nombre que ha creado anteriormente (tenga en cuenta que no aparece en la lista, pero se encontrará si busca el nombre completo).
1. Guarde el rol.

Espere de cinco a diez minutos antes de usar las credenciales para el montaje.

### <a name="set-environment-variable-for-oauth-credentials"></a>Establecimiento de la variable de entorno para las credenciales de OAuth

Abra un símbolo del sistema en un equipo cliente que pueda acceder al clúster de macrodatos. Establezca una variable de entorno con el siguiente formato: Tenga en cuenta que las credenciales deben estar en una lista separada por comas. El comando "set" se usa en Windows. Si usa Linux, utilice "export" en su lugar.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint],
    fs.azure.account.oauth2.client.id=[Application client ID],
    fs.azure.account.oauth2.client.secret=[client secret]
   ```

## <a name="use-access-keys-to-mount"></a>Uso de claves de acceso para el montaje

También puede llevar a cabo el montaje con las claves de acceso que puede obtener para la cuenta de ADLS en Azure Portal.

 > [!TIP]
   > Para obtener más información sobre cómo buscar la clave de acceso (`<storage-account-access-key>`) de la cuenta de almacenamiento, vea [Visualización de claves de cuenta y cadena de conexión](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Establecimiento de la variable de entorno para las credenciales de clave de acceso

1. Abra un símbolo del sistema en un equipo cliente que pueda acceder al clúster de macrodatos.

1. Abra un símbolo del sistema en un equipo cliente que pueda acceder al clúster de macrodatos. Establezca una variable de entorno con el siguiente formato. Tenga en cuenta que las credenciales deben estar en una lista separada por comas. El comando "set" se usa en Windows. Si usa Linux, utilice "export" en su lugar.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a> Montaje del almacenamiento de HDFS remoto

Ahora que ha establecido la variable de entorno MOUNT_CREDENTIALS para las claves de acceso o mediante OAuth, puede iniciar el montaje. En los pasos siguientes se monta el almacenamiento de HDFS remoto en Azure Data Lake en el almacenamiento de HDFS local del clúster de macrodatos.

1. Use **kubectl** para buscar la dirección IP del servicio **controller-svc-external** de punto de conexión en el clúster de macrodatos. Busque el valor de **External-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Inicie sesión con **azdata** mediante la dirección IP externa del punto de conexión del controlador con el nombre de usuario y la contraseña del clúster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080
   ```
1. Establezca la variable de entorno MOUNT_CREDENTIALS (desplácese hacia arriba para obtener instrucciones).

1. Monte el almacenamiento de HDFS remoto en Azure mediante la **creación del montaje de azdata BDC HDFS**. Reemplace los valores de marcador de posición antes de ejecutar el siguiente comando:

   ```bash
   azdata bdc hdfs mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > El comando mount create es asincrónico. En este momento, no hay ningún mensaje que indique si el montaje se ha realizado correctamente. Consulte la sección sobre el [estado](#status) para comprobar el estado de los montajes.

Si se ha montado correctamente, debería poder consultar los datos de HDFS y ejecutar trabajos de Spark en ellos. Aparecerán en el HDFS del clúster de macrodatos en la ubicación que especifique `--mount-path`.

## <a id="status"></a> Obtención del estado de los montajes

Para mostrar el estado de todos los montajes en el clúster de macrodatos, use el siguiente comando:

```bash
azdata bdc hdfs mount status
```

Para mostrar el estado de un montaje en una ruta de acceso específica de HDFS, use el siguiente comando:

```bash
azdata bdc hdfs mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Actualización de un montaje

En el siguiente ejemplo se actualiza el montaje. Esta actualización también borrará la memoria caché de montaje.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a> Eliminación del montaje

Para eliminar el montaje, use el comando **azdata BDC HDFS Mount Delete** y especifique la ruta de acceso de montaje en HDFS:

```bash
azdata bdc hdfs mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]acerca de, vea [¿Qué es [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
