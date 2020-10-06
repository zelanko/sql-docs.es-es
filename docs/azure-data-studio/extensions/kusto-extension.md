---
title: Extensión Kusto (KQL) para Azure Data Studio
description: En este artículo se explica cómo conectarse a clústeres de Azure Data Explorer y realizar consultas con Azure Data Studio.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: jukoesma
ms.custom: ''
ms.date: 09/22/2020
ms.openlocfilehash: 2ffe3945f8dd7e8c0ce9cf504c09622ca1a20331
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725194"
---
# <a name="kusto-kql-extension-for-azure-data-studio-preview"></a>Extensión Kusto (KQL) para Azure Data Studio (versión preliminar)

La extensión Kusto (KQL) para [Azure Data Studio](../what-is.md) permite conectarse a clústeres de [Azure Data Explorer](/azure/data-explorer/data-explorer-overview) y realizar consultas.

Los usuarios pueden escribir y ejecutar consultas de KQL, así como crear cuadernos con el [kernel de Kusto](../notebooks/notebooks-kusto-kernel.md) completado con IntelliSense.

Al habilitar la experiencia nativa de Kusto (KQL) en Azure Data Studio, los ingenieros, los científicos y los analistas de datos pueden observar rápidamente tendencias y anomalías en grandes cantidades de datos almacenados en Azure Data Explorer.

Esta extensión está actualmente en versión preliminar.

## <a name="prerequisites"></a>Requisitos previos

Si no tiene una suscripción a Azure, cree una [cuenta gratuita de Azure](https://azure.microsoft.com/free/) antes de empezar.

También se necesitan los siguientes requisitos previos:

- [Azure Data Studio instalado](../download-azure-data-studio.md).
- [Un clúster y la base de datos de Azure Data Explorer](/azure/data-explorer/create-cluster-database-portal).

## <a name="install-the-kusto-kql-extension"></a>Instalación de la extensión Kusto (KQL)

Para instalar la extensión Kusto (KQL) en Azure Data Studio, siga los pasos que se indican a continuación.

1. Abra el administrador de extensiones en Azure Data Studio. Puede seleccionar el icono de extensiones o seleccionar **Extensiones** en el menú Vista.

2. Escriba *Kusto* en la barra de búsqueda.

3. Seleccione la extensión **Kusto (KQL)** y vea sus detalles.

4. Seleccione **Instalar**.

:::image type="content" source="media/kusto-extension/kusto-extension-icon.png" alt-text="Extensión Kusto":::

## <a name="how-to-connect-to-an-azure-data-explorer-cluster"></a>Conexión a un clúster de Azure Data Explorer

### <a name="find-your-azure-data-explorer-cluster"></a>Búsqueda del clúster de Azure Data Explorer

Busque el clúster de Azure Data Explorer en [Azure Portal](https://ms.portal.azure.com/#home) y luego busque el URI del clúster.

:::image type="content" source="media/kusto-extension/kusto-extension-adx-cluster-uri.png" alt-text="Extensión Kusto":::

Pero puede empezar de inmediato con el clúster *help.kusto.windows.net*.

En este artículo se van a usar los datos del clúster help.kusto.windows.net para los ejemplos.

### <a name="connection-details"></a>Detalles de conexión

Para configurar un clúster de Azure Data Explorer al que conectarse, siga estos pasos.

1. Seleccione **Nueva conexión** en el panel **Conexiones**.

2. Rellene la información de **Detalles de conexión**.
    1. En **Tipo de conexión**, seleccione *Kusto*.
    2. En **Clúster**, especifique el clúster de Azure Data Explorer.

        > [!Note]
        > Al escribir el nombre del clúster, no incluya el prefijo `https://` ni una `/` final.

    3. En **Tipo de autenticación**, use la cuenta predeterminada *Azure Active Directory - Universal con MFA*.
    4. En **Cuenta**, use la información de la cuenta.
    5. En **Base de datos**, use *Predeterminada*.
    6. En **Grupo de servidores**, use *Predeterminado*.
        1. Puede usar este campo para organizar los servidores de un grupo concreto.
    7. Deje en blanco el campo **Nombre (opcional)** .
        1. Puede usar este campo para asignar un alias al servidor.

    :::image type="content" source="media/kusto-extension/kusto-extension-connection-details.png" alt-text="Extensión Kusto":::

## <a name="how-to-query-an-azure-data-explorer-database-in-azure-data-studio"></a>Consulta de una base de datos de Azure Data Explorer en Azure Data Studio

Ahora que ha configurado una conexión al clúster de Azure Data Explorer, puede realizar consultas a las bases de datos mediante Kusto (KQL).

Para crear una pestaña de nueva consulta, puede seleccionar **Archivo > Nueva consulta**, usar *Ctrl + N* o bien hacer clic con el botón derecho en la base de datos y seleccionar **Nueva consulta**.

Una vez abierta la pestaña de nueva consulta, escriba la consulta de Kusto.

Estos son algunos ejemplos de consultas de KQL:

```kusto
StormEvents
| limit 1000
```

```kusto
StormEvents
| where EventType == "Waterspout"
```

Para obtener más información sobre cómo escribir consultas de KQL, visite [Escritura de consultas para Azure Data Explorer](/azure/data-explorer/write-queries#overview-of-the-query-language)

## <a name="view-extension-settings"></a>Visualización de la configuración de la extensión

Para cambiar la configuración de la extensión Kusto, siga los pasos que se indican a continuación.

1. Abra el administrador de extensiones en Azure Data Studio. Puede seleccionar el icono de extensiones o seleccionar **Extensiones** en el menú Vista.

2. Busque la extensión **Kusto (KQL)** .

3. Seleccione el icono **Administrar**.

4. Seleccione el icono **Configuración de extensiones**.

La configuración de la extensión tiene este aspecto:

:::image type="content" source="media/kusto-extension/kusto-extension-settings.png" alt-text="Extensión Kusto":::

## <a name="sanddance-visualization"></a>Visualización de SandDance

La [extensión SandDance](../sanddance-extension.md) conjuntamente con la extensión Kusto (KQL) en Azure Data Studio aportan una visualización interactiva enriquecida. En el conjunto de resultados de consulta de KQL, seleccione el botón **Visualizador** para iniciar [SandDance](https://sanddance.js.org/).

:::image type="content" source="media/kusto-extension/kusto-extension-sanddance-demo.gif" alt-text="Extensión Kusto":::

## <a name="known-issues"></a>Problemas conocidos

| Detalles | Solución alternativa |
|---------|------------|
| [No funciona el viewlet de la conexión Kusto después de la recarga](https://github.com/microsoft/azuredatastudio/issues/12475). | N/D |
| [No se puede volver a establecer la conexión automáticamente](https://github.com/microsoft/azuredatastudio/issues/11830). | Desconéctese del clúster de Azure Data Explorer y vuelva a conectarse. |
| [Al actualizar el clúster de Kusto, la conexión no se vuelve a establecer correctamente](https://github.com/microsoft/azuredatastudio/issues/11824). | Desconéctese del clúster de Azure Data Explorer y vuelva a conectarse. |
| [La conexión a un clúster debe mostrar el panel del clúster en lugar de la base de datos](https://github.com/microsoft/azuredatastudio/issues/12549) | N/D |
| Para cada tabla de la base de datos del clúster de Azure Data solo hay una opción para **SELECT TOP 1000** en vez de **TAKE 10**. | N/D |

Puede enviar una [solicitud de característica](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=feature_request.md&title=) si quiere proporcionar comentarios al equipo de productos.  
Puede informar de un [error](https://github.com/microsoft/azuredatastudio/issues/new?assignees=&labels=&template=bug_report.md&title=) si quiere proporcionar comentarios al equipo de productos.

## <a name="next-steps"></a>Pasos siguientes

- [Creación y ejecución de un cuaderno de Kusto](../notebooks/notebooks-kusto-kernel.md)
- [Cuaderno de Kqlmagic en Azure Data Studio](../notebooks/notebooks-kqlmagic.md)
- [Hoja de referencia rápida de SQL a Kusto](/azure/data-explorer/kusto/query/sqlcheatsheet)
- [¿Qué es el Explorador de datos de Azure?](/azure/data-explorer/data-explorer-overview)
- [Uso de visualizaciones de SandDance](https://sanddance.js.org/)
