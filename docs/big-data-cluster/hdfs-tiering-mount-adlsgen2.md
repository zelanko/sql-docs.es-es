---
title: Montaje de ADLS Gen2 para los niveles de HDFS
titleSuffix: How to mount ADLS Gen2
description: En este artículo se explica cómo configurar la organización en niveles de HDFS para montar un sistema de archivos de Azure Data Lake Storage externo en HDFS en un clúster de macrodatos de SQL Server 2019 (versión preliminar).
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7d8a6dd53452700853dca9774ed0196ed7546fe
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419349"
---
# <a name="how-to-mount-adls-gen2-for-hdfs-tiering-in-a-big-data-cluster"></a>Cómo montar ADLS Gen2 para la organización en niveles de HDFS en un clúster de Big Data

En las secciones siguientes se proporciona un ejemplo de cómo configurar la organización en niveles de HDFS con un origen de datos de Azure Data Lake Storage Gen2.

## <a name="prerequisites"></a>Requisitos previos

- [Clúster de Big Data implementado](deployment-guidance.md)
- [Herramientas de macrodatos](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a id="load"></a>Cargar datos en Azure Data Lake Storage

En la siguiente sección se describe cómo configurar Azure Data Lake Storage Gen2 para probar la organización en niveles de HDFS. Si ya tiene datos almacenados en Azure Data Lake Storage, puede omitir esta sección para usar sus propios datos.

1. [Cree una cuenta de almacenamiento con capacidades de Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-quickstart-create-account).

1. [Cree un contenedor](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-portal) de blobs en esta cuenta de almacenamiento para los datos externos.

1. Cargue un archivo CSV o parquet en el contenedor. Estos son los datos de HDFS externos que se montarán en HDFS en el clúster de Big Data.

## <a name="credentials-for-mounting"></a>Credenciales para el montaje

## <a name="use-oauth-credentials-to-mount"></a>Usar credenciales de OAuth para montar

Para poder usar las credenciales de OAuth para montar, debe seguir los pasos siguientes:

1. Vaya a la [Azure portal](https://portal.azure.com)
1. Vaya a "servicios" en el panel de navegación izquierdo y el reloj en "Azure Active Directory"
1. Mediante "registros de aplicaciones" en el menú, cree una "aplicación web y siga el asistente. **Recuerde el nombre que cree aquí**. Tendrá que agregar este nombre a su cuenta de ADLS como usuario autorizado.
1. Una vez creada la aplicación Web, vaya a "claves" en "configuración" para la aplicación.
1. Seleccione una duración de clave y haga clic en guardar. **Guarde la clave generada.**
1.  Vuelva a la página registros de aplicaciones y haga clic en el botón "puntos de conexión" en la parte superior. **Anote la dirección URL del "extremo del token"**
1. Ahora debería tener en cuenta lo siguiente en OAuth:

    - "ID. de aplicación" de la aplicación web que creó anteriormente en el paso 3
    - La clave que acaba de generar en el paso 5
    - El punto de conexión del token del paso 6

### <a name="adding-the-service-principal-to-your-adls-account"></a>Adición de la entidad de servicio a la cuenta de ADLS

1. Vuelva al portal de nuevo y abra su cuenta de ADLS y seleccione control de acceso (IAM) en el menú de la izquierda.
1. Seleccione "agregar una asignación de roles" y busque el nombre que creó en Step3 anterior (tenga en cuenta que no aparece en la lista, pero se encontrará si busca el nombre completo).
1. Ahora, agregue el rol de "colaborador de datos de BLOB de almacenamiento (versión preliminar)".

Espere 5-10 minutos antes de usar las credenciales para el montaje

### <a name="set-environment-variable-for-oauth-credentials"></a>Establecer la variable de entorno para las credenciales de OAuth

Abra un símbolo del sistema en un equipo cliente que pueda tener acceso al clúster de Big Data. Establezca una variable de entorno con el siguiente formato: Tenga en cuenta que las credenciales deben estar en una lista separada por comas. El comando "SET" se usa en Windows. Si usa Linux, use "Export" en su lugar.

   ```text
    set MOUNT_CREDENTIALS=fs.azure.account.auth.type=OAuth,
    fs.azure.account.oauth.provider.type=org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider,
    fs.azure.account.oauth2.client.endpoint=[token endpoint from step6 above],
    fs.azure.account.oauth2.client.id=[<Application ID> from step3 above],
    fs.azure.account.oauth2.client.secret=[<key> from step5 above]
   ```

## <a name="use-access-keys-to-mount"></a>Usar claves de acceso para montar

También puede montar con las claves de acceso que puede obtener para la cuenta de ADLS en el Azure Portal.

 > [!TIP]
   > Para obtener más información sobre cómo buscar la clave de acceso`<storage-account-access-key>`() de la cuenta de almacenamiento, consulte [Ver claves de cuenta y cadena de conexión](/azure/storage/common/storage-account-manage#view-account-keys-and-connection-string).

### <a name="set-environment-variable-for-access-key-credentials"></a>Establecer la variable de entorno para las credenciales de clave de acceso

1. Abra un símbolo del sistema en un equipo cliente que pueda tener acceso al clúster de Big Data.

1. Abra un símbolo del sistema en un equipo cliente que pueda tener acceso al clúster de Big Data. Establezca una variable de entorno con el siguiente formato. Tenga en cuenta que las credenciales deben estar en una lista separada por comas. El comando "SET" se usa en Windows. Si usa Linux, use "Export" en su lugar.

   ```text
   set MOUNT_CREDENTIALS=fs.azure.abfs.account.name=<your-storage-account-name>.dfs.core.windows.net,
   fs.azure.account.key.<your-storage-account-name>.dfs.core.windows.net=<storage-account-access-key>
   ```

## <a id="mount"></a>Montaje del almacenamiento de HDFS remoto

Ahora que ha establecido la variable de entorno MOUNT_CREDENTIALS para las claves de acceso o el uso de OAuth, puede iniciar el montaje. En los pasos siguientes se monta el almacenamiento de HDFS remoto en Azure Data Lake al almacenamiento de HDFS local del clúster de Big Data.

1. Use **kubectl** para buscar la dirección IP del **controlador de punto de conexión: servicio SVC-external** en el clúster de Big Data. Busque **external-IP**.

   ```bash
   kubectl get svc controller-svc-external -n <your-big-data-cluster-name>
   ```

1. Inicie sesión con **azdata** mediante la dirección IP externa del punto de conexión del controlador con el nombre de usuario y la contraseña del clúster:

   ```bash
   azdata login -e https://<IP-of-controller-svc-external>:30080/
   ```
1. Establezca la variable de entorno MOUNT_CREDENTIALS (Desplácese hacia arriba para obtener instrucciones)

1. Monte el almacenamiento de HDFS remoto en Azure mediante el **almacenamiento de BDC de azdata creación del grupo de montaje**. Reemplace los valores de marcador de posición antes de ejecutar el siguiente comando:

   ```bash
   azdata bdc storage-pool mount create --remote-uri abfs://<blob-container-name>@<storage-account-name>.dfs.core.windows.net/ --mount-path /mounts/<mount-name>
   ```

   > [!NOTE]
   > El comando mount Create es asincrónico. En este momento, no hay ningún mensaje que indique si el montaje tuvo éxito. Consulte la sección [Estado](#status) para comprobar el estado de los montajes.

Si se monta correctamente, debería poder consultar los datos de HDFS y ejecutar trabajos de Spark en él. Aparecerá en HDFS para el clúster de Big Data en la ubicación especificada por `--mount-path`.

## <a id="status"></a>Obtención del estado de montajes

Para mostrar el estado de todos los montajes en el clúster de Big Data, use el siguiente comando:

```bash
azdata bdc storage-pool mount status
```

Para mostrar el estado de un montaje en una ruta de acceso específica en HDFS, use el siguiente comando:

```bash
azdata bdc storage-pool mount status --mount-path <mount-path-in-hdfs>
```

## <a name="refresh-a-mount"></a>Actualización de un montaje

En el ejemplo siguiente se actualiza el montaje.

```bash
azdata bdc hdfs mount refresh --mount-path <mount-path-in-hdfs>
```

## <a id="delete"></a>Eliminar el montaje

Para eliminar el montaje, use el comando **azdata BDC Storage-Pool Mount Delete** y especifique la ruta de acceso de montaje en HDFS:

```bash
azdata bdc storage-pool mount delete --mount-path <mount-path-in-hdfs>
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de macrodatos de SQL Server 2019, consulte [¿Qué son los clústeres de macrodatos de SQL Server 2019?](big-data-cluster-overview.md).
