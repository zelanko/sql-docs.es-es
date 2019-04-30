---
title: API de extensibilidad
titleSuffix: Azure Data Studio
description: Obtenga información sobre las API de extensibilidad para Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0a8177492de46c92577eb98e79ece42e77ba947b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63180216"
---
# <a name="azure-data-studio-extensibility-apis"></a>API de extensibilidad de Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] Proporciona una API que pueden usar extensiones para interactuar con otras partes de Azure Data Studio, como el Explorador de objetos. Estas API están disponibles desde el [ `src/sql/sqlops.d.ts` ](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.d.ts) de archivos y se describen a continuación.

## <a name="connection-management"></a>Administración de conexiones
`sqlops.connection`

### <a name="top-level-functions"></a>Funciones de nivel superior

- `getCurrentConnection(): Thenable<sqlops.connection.Connection>` Obtiene la conexión actual basándose en el editor activo o la selección del explorador de objetos.

- `getActiveConnections(): Thenable<sqlops.connection.Connection[]>` Obtiene una lista de todas las conexiones del usuario que están activas. Devuelve una lista vacía si no hay ningún dichas conexiones.

- `getCredentials(connectionId: string): Thenable<{ [name: string]: string }>` Obtiene un diccionario que contiene las credenciales asociadas con una conexión. En caso contrario, estas se devolverá como parte del diccionario de opciones en un `sqlops.connection.Connection` objeto pero obtener quitará dicho objeto. 

### `Connection`
- `options: { [name: string]: string }` El diccionario de las opciones de conexión
- `providerName: string` El nombre del proveedor de conexión (por ejemplo, "MSSQL")
- `connectionId: string` El identificador único para la conexión

### <a name="example-code"></a>Código de ejemplo
```
> let connection = sqlops.connection.getCurrentConnection();
connection: {
    providerName: 'MSSQL',
    connectionId: 'd97bb63a-466e-4ef0-ab6f-00cd44721dcc',
    options: {
        server: 'mairvine-sql-server',
        user: 'sa',
        authenticationType: 'sqlLogin',
        ...
    },
    ...
}
> let credentials = sqlops.connection.getCredentials(connection.connectionId);
credentials: {
    password: 'abc123'
}

```

## <a name="object-explorer"></a>Explorador de objetos

`sqlops.objectexplorer`


### <a name="top-level-functions"></a>Funciones de nivel superior
- `getNode(connectionId: string, nodePath?: string): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obtenga un nodo del explorador de objetos correspondiente a la conexión especificada y la ruta de acceso. Si no se especifica ninguna ruta de acceso, devuelve el nodo de nivel superior para la conexión especificada. Si no hay ningún nodo en la ruta de acceso especificada, devuelve `undefined`. Nota: El `nodePath` para un objeto generado por el back-end de servicio de las herramientas de SQL y es difícil de construir manualmente. Las futuras mejoras de API, podrá obtener nodos basados en los metadatos que proporcione sobre el nodo, como nombre, tipo y el esquema.

- `getActiveConnectionNodes(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obtener todos los nodos de conexión de explorador de objetos activos.

- `findNodes(connectionId: string, type: string, schema: string, name: string, database: string, parentObjectNames: string[]): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Buscar todos los nodos del explorador de objetos que coinciden con los metadatos dados. El `schema`, `database`, y `parentObjectNames` argumentos deben ser `undefined` cuando no son aplicables. `parentObjectNames` es una lista de objetos que no son de base de datos principal, del superior al nivel más bajo en el Explorador de objetos, que es el objeto deseado en. Por ejemplo, cuando se busca una columna "column1" que pertenece a una tabla "schema1.table1" y la base de datos "database1" con Id. de conexión `connectionId`, llame a `findNodes(connectionId, 'Column', undefined, 'column1', 'database1', ['schema1.table1'])`. Consulte también el [lista de tipos que admite Azure Data Studio predeterminada](https://github.com/Microsoft/azuredatastudio/wiki/Object-Explorer-types-supported-by-FindNodes-API) para esta llamada API.

### <a name="objectexplorernode"></a>ObjectExplorerNode
- `connectionId: string` El identificador de la conexión que el nodo existe en

- `nodePath: string` La ruta de acceso del nodo, como se utiliza para llamar a la `getNode` función.

- `nodeType: string` Una cadena que representa el tipo del nodo

- `nodeSubType: string` Una cadena que representa el subtipo del nodo

- `nodeStatus: string` Una cadena que representa el estado del nodo

- `label: string` La etiqueta del nodo tal y como aparece en el Explorador de objetos

- `isLeaf: boolean` Si el nodo es un nodo hoja y, por tanto, no tiene elementos secundarios

- `metadata: sqlops.ObjectMetadata` Metadatos que describen el objeto representado por este nodo

- `errorMessage: string` Mensaje que se muestra si el nodo está en un estado de error

- `isExpanded(): Thenable<boolean>` Si el nodo está expandido actualmente en el Explorador de objetos

- `setExpandedState(expandedState: vscode.TreeItemCollapsibleState): Thenable<void>` Establecer si el nodo está expandido o contraído. Si el estado se establece en None, no se cambiará el nodo.

- `setSelected(selected: boolean, clearOtherSelections?: boolean): Thenable<void>` Establecer si el nodo está seleccionado. Si `clearOtherSelections` es true, borre las otras selecciones al realizar la nueva selección. Si es false, deje las selecciones existentes. `clearOtherSelections` el valor predeterminado es true cuando `selected` es true y false cuando `selected` es false.

- `getChildren(): Thenable<sqlops.objectexplorer.ObjectExplorerNode[]>` Obtener a todos los secundarios de los nodos de este nodo. Devuelve una lista vacía si no hay ningún elemento secundario.

- `getParent(): Thenable<sqlops.objectexplorer.ObjectExplorerNode>` Obtiene el nodo primario de este nodo. Devuelve undefined si no hay ningún elemento primario.

### <a name="example-code"></a>Código de ejemplo

```cs
private async interactWithOENode(selectedNode: sqlops.objectexplorer.ObjectExplorerNode): Promise<void> {
    let choices = ['Expand', 'Collapse', 'Select', 'Select (multi)', 'Deselect', 'Deselect (multi)'];
    if (selectedNode.isLeaf) {
        choices[0] += ' (is leaf)';
        choices[1] += ' (is leaf)';
    } else {
        let expanded = await selectedNode.isExpanded();
        if (expanded) {
            choices[0] += ' (is expanded)';
        } else {
            choices[1] += ' (is collapsed)';
        }
    }
    let parent = await selectedNode.getParent();
    if (parent) {
        choices.push('Get Parent');
    }
    let children = await selectedNode.getChildren();
    children.forEach(child => choices.push(child.label));
    let choice = await vscode.window.showQuickPick(choices);
    let nextNode: sqlops.objectexplorer.ObjectExplorerNode = undefined;
    if (choice === choices[0]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Expanded);
    } else if (choice === choices[1]) {
        selectedNode.setExpandedState(vscode.TreeItemCollapsibleState.Collapsed);
    } else if (choice === choices[2]) {
        selectedNode.setSelected(true);
    } else if (choice === choices[3]) {
        selectedNode.setSelected(true, false);
    } else if (choice === choices[4]) {
        selectedNode.setSelected(false);
    } else if (choice === choices[5]) {
        selectedNode.setSelected(false, true);
    } else if (choice === 'Get Parent') {
        nextNode = parent;
    } else {
        let childNode = children.find(child => child.label === choice);
        nextNode = childNode;
    }
    if (nextNode) {
        let updatedNode = await sqlops.objectexplorer.getNode(nextNode.connectionId, nextNode.nodePath);
        this.interactWithOENode(updatedNode);
    }
}

vscode.commands.registerCommand('mssql.objectexplorer.interact', () => {
    sqlops.objectexplorer.getActiveConnectionNodes().then(activeConnections => {
        vscode.window.showQuickPick(activeConnections.map(connection => connection.label + ' ' + connection.connectionId)).then(selection => {
            let selectedNode = activeConnections.find(connection => connection.label + ' ' + connection.connectionId === selection);
            this.interactWithOENode(selectedNode);
        });
    });
});
```

## <a name="proposed-apis"></a>API de propuesta

Hemos agregado API propuestas para permitir las extensiones mostrar la interfaz de usuario personalizada en los cuadros de diálogo, asistentes y las pestañas de documentos, entre otras funciones. Consulte la [archivo propuesto de tipos de API](https://github.com/Microsoft/azuredatastudio/blob/master/src/sql/sqlops.proposed.d.ts) para obtener más documentación, aunque tenga en cuenta que estas API están sujetos a cambios en cualquier momento. Ejemplos de cómo utilizar algunas de estas API pueden encontrarse en el ["sqlservices" extensión de ejemplo](https://github.com/Microsoft/azuredatastudio/tree/master/samples/sqlservices).


