---
title: Extensión de la implementación de aplicación
titleSuffix: SQL Server 2019 big data clusters
description: Implementar un script de Python o R como una aplicación en clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 8f45817510cb63937544fa4f0f7af5bb42a0c883
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018471"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>Cómo utilizar VS Code para implementar aplicaciones en clústeres de macrodatos de SQL Server

En este artículo se describe cómo implementar aplicaciones en un clúster de macrodatos de SQL Server con Visual Studio Code con la extensión de la implementación de la aplicación. Esta funcionalidad se introdujo en CTP 2.3. 

## <a name="prerequisites"></a>Requisitos previos

- [Código de Visual Studio](https://code.visualstudio.com/).
- [Clúster de SQL Server macrodatos](big-data-cluster-overview.md) CTP 2.3 o posterior.

## <a name="capabilities"></a>Capabilities

Esta extensión admite las siguientes tareas en Visual Studio Code:

- Autenticar con el clúster de Macrodatos SQL Server.
- Recuperar una plantilla de aplicación desde el repositorio de GitHub para la implementación de runtimes compatibles.
- Administrar plantillas de aplicación abierto actualmente en el área de trabajo del usuario.
- Implementar una aplicación a través de una especificación de formato YAML.
- Administrar las aplicaciones implementadas en el clúster grande de datos de SQL Server.
- Ver todas las aplicaciones que haya implementado en la barra lateral con información adicional.
- Generar una especificación de ejecución para utilizar la aplicación o eliminar la aplicación desde el clúster.
- Consumir las aplicaciones implementadas a través de una especificación de ejecución YAML.

Las secciones siguientes aunque recorrer el proceso de instalación y proporciona información general sobre cómo funciona la extensión. 

### <a name="install"></a>Install

En primer lugar, instale la extensión de la implementación de aplicaciones en VS Code:

1. Descargar [extensión de implementar la aplicación](https://aka.ms/app-deploy-vscode) para instalar la extensión como parte del código de VS.

1. Inicie VS Code y vaya a la barra lateral de extensiones.

1. Haga clic en el `…` menú contextual en la parte superior de la barra lateral y seleccione `Install from vsix`.

   ![Instalación de VSIX](media/vs-extension/install_vsix.png)

1. Buscar el `sqlservbdc-app-deploy.vsix` archivo que descargó y elija que se va a instalar.

Después de implementar la aplicación de clúster de macrodatos de SQL Server se ha instalado la extensión, le pedirá que vuelva a cargar VS Code. Ahora debería ver el Explorador de aplicación de BDC de SQL Server en la barra lateral de VS Code.

### <a name="app-explorer"></a>Aplicación de explorador

Haga clic en la extensión en la barra lateral para cargar un panel lateral que muestra el Explorador de la aplicación. La siguiente captura de pantalla del explorador de la aplicación de ejemplo muestra ningún aplicaciones o las especificaciones de aplicación disponibles:

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>Nueva conexión

Para conectarse al punto de conexión de clúster, use uno de los métodos siguientes:

- Haga clic en la barra de estado en la parte inferior que dice `SQL Server BDC Disconnected`.
- O haga clic en el `New Connection` situado en la parte superior de la flecha que apunta a una puerta de entrada.

   ![Nueva conexión](media/vs-extension/connect_to_cluster.png)

VS Code le pide el punto de conexión adecuado, el nombre de usuario y la contraseña. Si no especifica las credenciales correctas y el punto de conexión de aplicación, VS Code le notifica que se conectó al clúster y verá que las aplicaciones implementadas que se rellena en la barra lateral. Si se conecta correctamente, el nombre de usuario y el punto de conexión se guardará en `./sqldbc` como parte del perfil de usuario. Nunca se guardará ninguna contraseña ni símbolos (tokens). Al iniciar sesión de nuevo, el símbolo del sistema se rellene previamente con el host de guardado y el nombre de usuario, pero siempre requieren que escriba una contraseña. Si desea conectarse a un punto de conexión de clúster diferente, simplemente haga clic en el `New Connection` nuevo. La conexión se cerrará automáticamente si cierre VS Code o abra otra área de trabajo y deberá volver a conectar.

### <a name="app-template"></a>Plantilla de aplicación

Para implementar una aplicación desde una de nuestras plantillas, haga clic en el `New App Template` situado en la `App Specifications` panel, donde se le pedirá para el nombre, el tiempo de ejecución y en qué ubicación desea colocar la nueva aplicación en el equipo local. Se aconseja que colocarlo en el área de trabajo actual de VS Code para que puede usar la funcionalidad completa de la extensión, pero puede colocarlo en cualquier lugar en el sistema de archivos local.

![Nueva plantilla de aplicación](media/vs-extension/new_app_template.png)

Una vez completado, una nueva plantilla de aplicación se ha aplicado scaffolding para usted en la ubicación especificada y la implementación de `spec.yaml` se abre en el área de trabajo. Si el directorio que seleccionó está en el área de trabajo, también verá que aparece bajo el `App Specifications` panel:

![Cargar plantilla de aplicación](media/vs-extension/loading_app_template.png)

La plantilla es una sencilla `Hello World` aplicación que se distribuyen como sigue:

- **spec.yaml**
   - El clúster enseña a implementar la aplicación
- **run-spec.yaml**
   - Indica al clúster cómo gustaría llamar a la aplicación
- **handler.py**
   - Se trata de su archivo de código fuente según lo especificado por `src` en `spec.yaml`
   - Tiene una función llamada `handler` que se considera el `entrypoint` de la aplicación, como se muestra en `spec.yaml`. Toma una entrada de cadena llamada `msg` y devuelve una cadena de salida denominada `out`. Se especifican en `inputs` y `outputs` de la `spec.yaml`.

Si no desea que una plantilla con scaffolding y sería preferible simplemente un `spec.yaml` para la implementación de una aplicación que ya ha creado, haga clic en el `New Deploy Spec` situado junto a la `New App Template` botón así pues, siga el mismo proceso, pero solo recibirá la `spec.yaml`, que se puede modificar cómo se elige.

### <a name="deploy-app"></a>Implementación de aplicación

Puede implementar esta aplicación desde el prisma de código al instante `Deploy App` en el `spec.yaml` o presione el botón de la carpeta de rayo junto a la `spec.yaml` archivo en el menú de las especificaciones de la aplicación. La extensión se comprima todos los archivos en el directorio donde su `spec.yaml` se encuentra e implementar su aplicación en el clúster. 

>[!NOTE]
>Asegúrese de que todos los archivos de aplicación están en el mismo directorio que su `spec.yaml`. El `spec.yaml` debe estar en el nivel raíz de su directorio de código fuente de aplicación. 

![Implementar el botón de la aplicación](media/vs-extension/deploy_app_lightning.png)

![Implementar aplicación de Codelens](media/vs-extension/deploy_app_codelens.png)

Se le notificará cuando la aplicación está lista para su uso en función del estado de la aplicación en la barra lateral:

![Aplicación implementada](media/vs-extension/app_deploy.png)

![Barra lateral de la aplicación listo](media/vs-extension/app_ready_side_bar.png)

![Notificación de aplicación preparada](media/vs-extension/app_ready_notification.png)

En el panel del lado, podrá ver el siguiente disponible para usted:

Puede ver todas las aplicaciones que haya implementado en la barra lateral con la siguiente información:

- state
- version
- parámetros de entrada
- Parámetros de salida
- Vínculos
  - swagger
  - detalles

Si hace clic en `Links`, verá que puede tener acceso a la `swagger.json` de la aplicación implementada, así que escribir sus propios clientes que llaman a la aplicación:

![Swagger](media/vs-extension/swagger.png)

### <a name="app-run"></a>Ejecución de la aplicación

Una vez que la aplicación esté lista, llamar a la aplicación con el `run-spec.yaml` que se proporcionó como parte de la plantilla de aplicación:

![Especificación de ejecución](media/vs-extension/run_spec.png)

Especifique cualquier cadena que desee en lugar de `hello` y, a continuación, vuelva a ejecutarla mediante el vínculo de la lente de código o en la barra lateral en el botón de rayo junto a la `run-spec.yaml`. Si no tiene una especificación de ejecución por cualquier motivo, generar uno a partir de la aplicación implementada en el clúster:

![Obtener ejecución especificación](media/vs-extension/get_run_spec.png)

Una vez que tiene uno y editado a su gusto, ejecútelo. VS Code devuelve la información apropiada cuando la aplicación ha terminado de ejecutarse:

![Salida de la aplicación](media/vs-extension/app_output.png)

Como puede ver en lo anterior, el resultado se exprese en un archivo temporal `.json` archivo en el área de trabajo. Si desea mantener esta salida, no dude en guardarlo, en caso contrario, se eliminará en el cierre. Si la aplicación no tiene una salida para imprimir en un archivo, sólo obtendrá la `Successful App Run` notificación en la parte inferior. Si no tenía una ejecución correcta, recibirá un mensaje de error correspondiente que le ayudarán a determinar cuál es el problema.

Cuando se ejecuta una aplicación, hay varias maneras para pasar parámetros:

Puede especificar todas las entradas necesarias a través de un `.json`, es decir:

- `inputs: ./example.json`

Al llamar a una aplicación implementada, si los parámetros de entrada son innata a la aplicación o usuario especificado y que dado el parámetro de entrada no es un tipo primitivo, como una matriz, vector, trama de datos, texto JSON, etc. especifica el tipo de parámetro directamente en línea cuando una llamada a la aplicación, es decir:

- Vector
    - `inputs:`
        - `x: [1, 2, 3]`
- Matriz
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Objeto
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

O proporcionar una cadena como una ruta de acceso relativa o absoluta a un `.txt`, `.json`, o `.csv` que proporciona la entrada necesaria en el formato que requiere la aplicación. El análisis del archivo se basa en `Node.js Path library`, donde se define una ruta de acceso de archivo como un `string that contains a / or \ character`.

Si no se proporciona el parámetro de entrada según sea necesario, se mostrará un mensaje de error con la ruta de acceso de archivo incorrecto si se proporcionó una ruta de acceso del archivo de cadena o ese parámetro no es válido. Se asigna la responsabilidad al creador de la aplicación para asegurarse de que entienden los parámetros que está definiendo.

Para eliminar una aplicación, simplemente haga clic en la Papelera puede situado junto a la aplicación en el `Deployed Apps` panel lateral.

## <a name="next-steps"></a>Pasos siguientes

También puede hacer referencia a los ejemplos adicionales en [ejemplos de implementación de aplicaciones](https://aka.ms/sql-app-deploy) para probar con la extensión.

Para obtener más información acerca de los clústeres de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).


Nuestro objetivo es hacer que esta extensión útiles para usted y le agradeceremos cualquier comentario. Envíelos a [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] equipo](https://aka.ms/sqlfeedback).
