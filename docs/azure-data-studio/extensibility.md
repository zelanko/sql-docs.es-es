---
title: Agregar funcionalidad adicional a través de la extensibilidad
titleSuffix: Azure Data Studio
description: Obtenga información sobre las áreas de extensibilidad clave para ampliar la funcionalidad de Azure Data Studio y el modelo de extensibilidad
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: ce80ae9ec15fc7e1fdf8c68b595c71b2ee3f0a64
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105041"
---
# <a name="getting-started-with-includename-sosincludesname-sos-shortmd-extensibility"></a>Introducción a [!INCLUDE[name-sos](../includes/name-sos-short.md)] extensibilidad

[!INCLUDE[name-sos](../includes/name-sos.md)] tiene varios mecanismos de extensibilidad para personalizar la experiencia del usuario y realizar esas personalizaciones disponibles para la Comunidad de usuarios todo. El núcleo [!INCLUDE[name-sos](../includes/name-sos.md)] plataforma se basa en el código de Visual Studio, por lo que la mayoría de las API de extensibilidad de Visual Studio Code están disponibles. Además, hemos proporcionado puntos de extensibilidad adicional para las actividades específicas de administración de datos.

Algunos de los puntos de extensibilidad clave son:

- Extensibilidad de Visual Studio Code API
- Herramientas de creación de la extensión de Azure Data Studio
- Administrar las contribuciones de panel de ficha de panel
- Información detallada con experiencias de acciones
- API de extensibilidad de Azure Data Studio
- API del proveedor de datos personalizados

## <a name="visual-studio-code-extensibility-apis"></a>Extensibilidad de Visual Studio Code API

Dado que el núcleo [!INCLUDE[name-sos](../includes/name-sos.md)] plataforma se basa en el código de Visual Studio, detalles sobre las API de extensibilidad de Visual Studio Code se encuentran en el [Extension Authoring](https://code.visualstudio.com/docs/extensions/overview) y [API de extensión](https://code.visualstudio.com/docs/extensionAPI/overview) documentación en el sitio Web de Visual Studio Code.

## <a name="manage-dashboard-tab-panel-contributions"></a>Administrar las contribuciones de panel de ficha de panel

Para obtener más información, consulte [contribución puntos](#contribution-points) y [Variables de contexto](#context-variables).

## <a name="azure-data-studio-extensibility-apis"></a>API de extensibilidad de Azure Data Studio

Para obtener más información, consulte [API de extensibilidad](extensibility-apis.md).


## <a name="contribution-points"></a>Puntos de contribución

En esta sección se trata los diversos puntos de contribución que se definen en el manifiesto de la extensión package.json.

IntelliSense se admite dentro de azuredatastudio.

## <a name="contributes-dashboard"></a>Contribuye panel

Contribuir pestaña, el contenedor, el widget de información al panel.

![Panel](media/extensibility/dashboard-page.png)

`dashboard.tabs`

Dashboard.Tabs crea las secciones de la pestaña dentro de la página del panel. Espera un objeto o una matriz de objetos.  

```json
"dashboard.tabs": [
{
    "id": "test-tab1",
    "title": "Test 1",
    "description": "The test 1 displays a list of widgets.",
    "when": "connectionProvider == 'MSSQL' && !mssql:iscloud",
    "alwaysShow": true,
    "container": {
        ...
    }
}
]
```

`dashboard.containers`

En lugar de especificar panel contenedor insertadas (dentro de la dashboard.tab). Puede registrar los contenedores mediante dashboard.containers. Acepta un objeto o una matriz del objeto.

```json
"dashboard.containers": [
{
    "id": "innerTab1",
    "container": {
        ...
    }
},
{
    "id": "innerTab2",
    "container": {
       ...
    }
}
]
```

Para hacer referencia al contenedor registrado, especifique el identificador del contenedor

```json
"dashboard.tabs": [
{
    ...
    "container": {
        "innerTab1": {             
        }
    }
}
]

```

`dashboard.insights`

Puede registrar información mediante dashboard.insights. Esto es similar a [Tutorial: Crear un widget de datos personalizados](https://docs.microsoft.com/sql/sql-operations-studio/tutorial-build-custom-insight-sql-server)

```json
"dashboard.insights": {
"id": "my-widget"
"type": {
    "count": {
        "dataDirection": "vertical",
        "dataType": "number",
        "legendPosition": "none",
           "labelFirstColumn": false,
        "columnsAsLabels": false
       }
   },
   "queryFile": "{your file folder}/activeSession.sql"
}
```


### <a name="dashboard-container-types"></a>Tipos de contenedor de panel

Actualmente, hay cuatro tipos de contenedor admitidos:

1. `widgets-container`

    ![Contenedor de widgets](media/extensibility/widgets-container.png)

    La lista de los widgets que se mostrará en el contenedor. Es un diseño de flujo. Acepta la lista de los widgets.

    ```json
    "container": {
        "widgets-container": [
        {
            "widget": {
                "query-data-store-db-insight": {
                }
            }
        },
        {
            "widget": {
                "explorer-widget": {
                }
            }
        }
      ]
    }
    ```

2. `webview-container`

    ![contenedor de WebView](media/extensibility/webview-container.png)

    Se mostrará la vista Web en todo el contenedor. Se espera que el Id. de objeto webview para ser el mismo Id. de la ficha

    ```json
    "container": {
        "webview-container": null
    }
    ```

3. `grid-container`

   ![contenedor de cuadrícula](media/extensibility/grid-container.png)

   La lista de vistas Web que se mostrará en el diseño de cuadrícula o de widgets

    ```json
    "container": {
        "grid-container": [
        {
            "name": "widget 1",
            "widget": {
                "explorer-widget": {
                }
            },
            "row":0,
            "col":0
        },
        {
            "name": "widget 2",
            "widget": {
                "tasks-widget": {
                    "backup", 
                    "restore",
                    "configureDashboard",
                    "newQuery"
                }
            },
            "row":0,
            "col":1
        },
        {
            "name": "Webview 1",
            "webview": {
                "id": "google"
            },
            "row":1,
            "col":0,
            "colspan":2
        },
        {
            "name": "widget 3",
            "widget": {
                "explorer-widget": {}
            },
            "row":0,
            "col":3,
            "rowspan":2
        },
    ]
    ```

4.  `nav-section`

    ![sección de la barra de navegación](media/extensibility/nav-section.png)

    La sección de exploración se mostrará en el contenedor

    ```json
    "container": {
        "nav-section": [
            {
                "id": "innerTab1",
                "title": "inner-tab1",
                "icon": {
                    "light": "./icons/tab1Icon.svg",
                    "dark": "./icons/tab1Icon_dark.svg"
                }
                "container": {
                    ...
                }
            },
            {
                "id": "innerTab2",
                "title": "inner-tab2",
                "icon": {
                    "light": "./icons/tab2Icon.svg",
                    "dark": "./icons/tab2Icon_dark.svg"
                }
                "container": {
                    ...
                }
            }
        ]
    }
    ```



## <a name="context-variables"></a>Variables de contexto

Para obtener información general acerca del contexto en el código de Visual Studio y, posteriormente, Azure Data Studio, consulte [extensibilidad](https://code.visualstudio.com/docs/extensionAPI/extension-points#_example).

En Azure Data Studio, tenemos un contexto específico en torno a las conexiones de base de datos disponibles para las extensiones.

### <a name="dashboard"></a>Panel

En el panel, se proporcionan las siguientes variables de contexto:

|variable de contexto| description|
|:---|:---|
|`connectionProvider` | Una cadena del identificador para el proveedor de la conexión actual. Por ejemplo, `connectionProvider == 'MSSQL'` |
|`serverName`|Una cadena del nombre del servidor de la conexión actual. Por ejemplo, `serverName == 'localhost'` |
|`databaseName` | Una cadena del nombre de base de datos de la conexión actual. Por ejemplo, `databaseName == 'master'` |
|`connection` | El objeto de perfil de conexión completa para la conexión actual (IConnectionProfile)|
|`dashboardContext` | Una cadena del contexto de la página del panel está actualmente. 'Database' o 'server'. Por ejemplo, `dashboardContext == 'database'`|
