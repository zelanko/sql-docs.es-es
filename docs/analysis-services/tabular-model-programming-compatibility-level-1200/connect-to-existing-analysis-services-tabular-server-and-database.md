---
title: Conectarse al servidor Tabular de Analysis Services existente y la base de datos | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 13900e4aaad52d39a2691fb40d0e419f55f660fc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38033395"
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>Conectarse a la base de datos y el servidor Tabular de Analysis Services existente
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
En SQL Server 2016, Analysis Services Management Objects (AMO) incluye varios espacios de nombres que podrían usarse para establecer una conexión de servidor. En este artículo se explica cómo establecer una conexión de servidor mediante el espacio de nombres Microsoft.AnalysisServices.Tabular para los modelos y bases de datos creadas de 1200 o nivel de compatibilidad superior. 

Para conectarse a un servidor de Analysis Services, el código debe crear una instancia de un objeto de servidor y, a continuación, llame al método Connect en él. Una vez conectado, las propiedades del objeto Server reflejará la configuración de la instancia actual de Analysis Services. 

Las siguientes clases se pueden usar para las conexiones de nivel superior: 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

Como puede ver, dos espacios de nombres proporcionan conectividad a los objetos de servidor y base de datos: el espacio de nombres Microsoft.AnalysisServices original para AMO y el nuevo espacio de nombres Microsoft.AnalysisServices.Tabular para TOM.

¿Por qué dos espacios de nombres para las mismas operaciones? La respuesta se encuentra descendente, en el nivel de base de datos y el modelo, donde la jerarquía de objetos se convierte en el modo específico y el árbol del modelo se compone de metadatos Multidimensional o Tabular. Para realizar llamadas en el árbol del modelo, se proporciona el objeto de servidor o base de datos para ambos tipos de modelos.

> [!NOTE]  
>  Los metadatos se usan para las operaciones y la definición del modelo están completamente diferente para los dos modos. Al separar el lenguaje de definición de datos (DDL) en dos espacios de nombres independientes, se ha simplificado la experiencia de desarrollo a través de la presentación de solo la API necesaria para un tipo de modelo específico. 

Aunque el DDL es diferente, las conexiones a un servidor son los mismos en todos los modos, las versiones y ediciones. Compatibilidad con un servidor y la conexión de base de datos a través de cualquier espacio de nombres le permite escribir herramientas genéricas o script que se conectan a cualquier instancia de Analysis Services o base de datos, sin tener que saber qué tipo de modelo está hospedado en el servidor.  

Esta flexibilidad explica las dependencias entre los ensamblados. Para realizar llamadas a por debajo del nivel de base de datos (por ejemplo, en un modelo dentro de una base de datos Tabular 1200, o en un cubo, dimensión o MeasureGroup dentro de una base de datos de 1050-1103 Tabular o Multidimensional), AMO tiene una dependencia de TOM. 

En cambio, TOM no tiene dependencias en AMO. Aunque TOM no puede usarse para explorar metadatos multidimensionales (cubos), se puede usar AMO para explorar Multidimensional y metadatos tabulares. 

Por este motivo, el primer paso para configurar el proyecto requiere agregar las referencias a todos los ensamblados AMO. Consulte [instalar, referencia y distribuye la biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obtener más información. 

> [!NOTE]  
>  Las conexiones de servidor y base de datos se basan en las clases AMO heredadas que heredan de MajorObject. Aunque no se utilizan objetos principales y secundarios en un árbol de modelo Tabular, la clase de objeto MajorObject es visible como una clase base para los objetos de servidor y base de datos, independientemente de qué API usar para establecer la conexión.  

## <a name="code-example-server-connection"></a>Ejemplo de código: conexión de servidor 

A continuación es un ejemplo de código C# que muestra cómo conectarse a una instancia de Analysis Services local y mostrar sus propiedades en una ventana de consola. 

En este ejemplo se muestra solo algunas de las propiedades de un objeto de servidor, pero hay otras propiedades disponibles, como ServerMode y DefaultCompatibilityLevel.  

```
using System; 
using Microsoft.AnalysisServices.Tabular; 

namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 


            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 

 
                Console.WriteLine("Connection established successfully."); 
                Console.WriteLine(); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.WriteLine("Server name:\t\t{0}", server.Name); 
                Console.WriteLine("Server product name:\t{0}", server.ProductName); 
                Console.WriteLine("Server product level:\t{0}", server.ProductLevel); 
                Console.WriteLine("Server version:\t\t{0}", server.Version); 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```
Al ejecutar este programa, el resultado muestra las propiedades en el objeto de servidor en una ventana de consola. 

## <a name="authentication-and-authorization"></a>Autenticación y autorización 

Un servidor o conexión de base de datos con Analysis Services requiere permisos administrativos, que se usa para las operaciones de lectura y escritura y para pasar a través de una solicitud de conexión suplantada.  

Aunque se ha ampliado la infraestructura de seguridad de Analysis Services en los últimos años para permitir la autenticación personalizada en condiciones muy específicas, el método de autenticación externo compatible solo es la seguridad integrada de Windows. Las entidades de seguridad se supone que Windows dominio usuario o grupo de cuentas válidas.  

En Windows 2012 y versiones posteriores, la delegación puede fluir entre dominios. En Analysis Services, la delegación solo se usa para los modelos DirectQuery en caso contrario, las conexiones son suplantadas o directa. 

## <a name="next-steps"></a>Pasos siguientes 

Después de establecer una conexión, el siguiente paso lógico es cualquier enumerar bases de datos existente en el servidor, o quizás cree una nueva base de datos vacía. Los vínculos siguientes son ejemplos de código que muestran ambas tareas básicas: 

- [Crear e implementar una base de datos vacía](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [Lista de bases de datos existentes](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
