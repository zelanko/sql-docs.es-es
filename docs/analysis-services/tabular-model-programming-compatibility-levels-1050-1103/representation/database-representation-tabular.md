---
title: Base de datos (tabular) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b6a55afa2c152fe5a97c474f0a23af1fda12ff57
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="database-representationtabular"></a>Representación de la base de datos (tabular)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  En el modo Tabular, la base de datos es el contenedor para todos los objetos en el modelo tabular.  
  
## <a name="database-representation"></a>Representación de la base de datos  
 La base de datos es el lugar donde residen todos los objetos que forman un modelo tabular. Contenidos en la base de datos, el desarrollador encuentra objetos como conexiones, tablas, roles y muchos otros.  
  
### <a name="database-in-amo"></a>Base de datos en AMO  
 Cuando use AMO para administrar una base de datos de modelo tabular, el objeto <xref:Microsoft.AnalysisServices.Database> de AMO coincide de forma unívoca con el objeto lógico de base de datos de un modelo tabular.  
  
> [!NOTE]  
>  Para obtener acceso a un objeto de base de datos, en AMO, el usuario necesita tener acceso a un objeto de servidor y conectarse a él.  
  
### <a name="database-in-adomdnet"></a>Base de datos en ADOMD.Net  
 Cuando se usa ADOMD para consultar una base de datos de modelo tabular, la conexión con una base de datos específica se obtiene a través del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>.  
  
 Puede conectarse directamente a una base de datos determinada mediante el fragmento de código siguiente:  
  
```csharp  
using ADOMD = Microsoft.AnalysisServices.AdomdClient;  
…  
   ADOMD.AdomdConnection currrentCnx = new ADOMD.AdomdConnection("Data Source=<<server\instance>>;Catalog=<<database>>");  
   currrentCnx.Open();  
…  
  
```  
  
 Además, en un objeto de conexión existente (que no se ha cerrado) puede cambiar la base de datos actual por otra como se muestra en el fragmento de código siguiente:  
  
```csharp  
currentCnx.ChangeDatabase("myOtherDatabase");  
  
```  
  
## <a name="database-in-amo"></a>Base de datos en AMO  
 Cuando se usa AMO para administrar un objeto de base de datos, comience con un objeto <xref:Microsoft.AnalysisServices.Server>. Después, busque la base de datos en la colección de bases de datos o cree una nueva base de datos agregando una a la colección.  
  
 En el fragmento de código siguiente se muestran los pasos necesarios para conectarse a un servidor y crear una base de datos vacía después de comprobar que la base de datos no existe:  
  
```  
  
AMO.Server CurrentServer = new AMO.Server();  
try  
{  
    CurrentServer.Connect(currentServerName);  
}  
catch (Exception cnxException)  
{  
    MessageBox.Show(string.Format("Error while trying to connect to server: [{0}]\nError message: {1}", currentServerName, cnxException.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    return;  
}  
newDatabaseName = DatabaseName.Text;  
if (CurrentServer.Databases.Contains(newDatabaseName))  
{  
    return;  
}  
try  
{  
    AMO.Database newDatabase = CurrentServer.Databases.Add(newDatabaseName);  
  
    CurrentServer.Update();  
}  
catch (Exception createDBxc)  
{  
    MessageBox.Show(String.Format("Database [{0}] couldn't be created.\n{1}", newDatabaseName, createDBxc.Message), "AMO to Tabular message", MessageBoxButtons.OK, MessageBoxIcon.Error);  
    newDatabaseAvailable = false;  
}  
  
```  
  
 Para tener un conocimiento práctico sobre cómo usar AMO para crear y manipular representaciones de la base de datos, vea el código fuente del ejemplo AMO 2012 Tabular; concreto, revise el siguiente archivo fuente: Database.cs. El ejemplo está disponible en Codeplex. El código de ejemplo se proporciona únicamente como apoyo a los conceptos lógicos explicados aquí y no se debe usar en un entorno de producción.  
  
  
