---
title: Conectarse a la base de datos y de servidor Tabular de Analysis Services existente | Documentos de Microsoft
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 05be704e-4ee4-4101-b5ce-96fdda18c639
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 05b577c5ea50c6c9749221ad9d2f352b970ba62d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-existing-analysis-services-tabular-server-and-database"></a>Conectarse a la base de datos y servidor Tabular de Analysis Services existente
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
En SQL Server 2016, objetos de administración de servicios de análisis (AMO) incluye varios espacios de nombres que pudieron usarse para configurar una conexión de servidor. Este artículo explica cómo establecer una conexión al servidor mediante el espacio de nombres Microsoft.AnalysisServices.Tabular para los modelos y bases de datos creadas en 1200 o nivel de compatibilidad superior. 

Para conectarse a un servidor de Analysis Services, el código debe crear una instancia de un objeto de servidor y, a continuación, llame al método Connect en él. Una vez conectado, propiedades del objeto Server reflejará la configuración de la instancia actual de Analysis Services. 

Las clases siguientes se pueden usar para las conexiones de nivel superior: 

* Microsoft.AnalysisServices.Server 
* Microsoft.AnalysisServices.Database 
* Microsoft.AnalysisServices.Tabular.Server 
* Microsoft.AnalysisServices.Tabular.Database 

Como puede ver, dos espacios de nombres proporcionan conectividad a los objetos de servidor y base de datos: el espacio de nombres Microsoft.AnalysisServices original para AMO y el nuevo espacio de nombres Microsoft.AnalysisServices.Tabular para TOM.

¿Por qué dos espacios de nombres para las mismas operaciones? La respuesta se encuentra siguen en la cadena, en el nivel de la base de datos y el modelo, donde la jerarquía de objetos se convierte en el modo específico y el árbol del modelo se compone de metadatos Multidimensional o Tabular. Para realizar llamadas en el árbol del modelo, se proporciona el objeto de servidor o base de datos para ambos tipos de modelo.

> [!NOTE]  
>  Los metadatos utilizados para las operaciones y la definición de modelo son completamente diferentes para los dos modos. Al separar el lenguaje de definición de datos (DDL) en dos espacios de nombres independientes, se simplifica la experiencia de desarrollo a través de la presentación de solo la API necesaria para un tipo de modelo específico. 

Aunque el DDL es diferente, las conexiones a un servidor son los mismos en todos los modos, las versiones y ediciones. Compatibilidad con un servidor y una conexión de base de datos a través de cualquier espacio de nombres le permite escribir herramientas genéricas o script que se conectan a una instancia de Analysis Services o base de datos, sin tener que saber qué tipo de modelo se hospeda en el servidor.  

Esta flexibilidad explica las dependencias entre los ensamblados. Para realizar llamadas por debajo del nivel de base de datos (por ejemplo, en un modelo dentro de una base de datos tabulares de 1200 o en un cubo, dimensión o MeasureGroup dentro de una base de datos de 1050-1103 Multidimensional o Tabular), AMO tiene una dependencia de TOM. 

En cambio, TOM no tiene dependencia en AMO. Aunque TOM no se puede usar para explorar metadatos multidimensionales (cubos), AMO puede usarse para explorar metadatos Tabular y Multidimensional. 

Por este motivo, el primer paso para configurar el proyecto requiere agregar referencias a todos los ensamblados AMO. Vea [instalar, referencia y distribuye la biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md) para obtener más información. 

> [!NOTE]  
>  Las conexiones de servidor y base de datos se basan en las clases AMO heredadas que se heredan de MajorObject. Aunque no se utilizan objetos principales y secundarios en un árbol de modelo Tabular, la clase MajorObject es visible como una clase base para objetos de servidor y base de datos, independientemente de la API que se usan para establecer la conexión.  

## <a name="code-example-server-connection"></a>Ejemplo de código: conexión de servidor 

A continuación se muestra un ejemplo de código C# que muestra cómo conectarse a una instancia de Analysis Services local y mostrar sus propiedades en una ventana de consola. 

Este ejemplo muestra solo algunas de las propiedades de un objeto de servidor, pero hay más propiedades disponibles, incluido ServerMode y DefaultCompatibilityLevel.  

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
Al ejecutar este programa, el resultado muestra propiedades en el objeto de servidor en una ventana de consola. 

## <a name="authentication-and-authorization"></a>Autenticación y autorización 

Un servidor o una conexión de base de datos para Analysis Services requiere permisos administrativos, que se usa para las operaciones de lectura y escritura y para pasar a través de una solicitud de conexión suplantada.  

Aunque se ha ampliado la infraestructura de seguridad de Analysis Services en los últimos años para permitir la autenticación personalizada en condiciones muy específicas, el método de autenticación externo compatible solo es seguridad integrada de Windows. Se supone que las entidades de seguridad son válidos usuario o grupo de cuentas de dominio Windows.  

En Windows 2012 y versiones posteriores, la delegación puede fluir entre dominios. En Analysis Services, la delegación solo se usa para los modelos DirectQuery; de lo contrario, las conexiones son directa o suplantado. 

## <a name="next-steps"></a>Pasos siguientes 

Después de establecer una conexión, el siguiente paso lógico es cualquier enumerar bases de datos existente en el servidor o es posible crear una nueva base de datos vacía. Los vínculos siguientes son ejemplos de código que muestran ambas tareas básicas: 

- [Crear e implementar una base de datos vacía](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md)
- [Lista de bases de datos existentes](../../analysis-services/tabular-model-programming-compatibility-level-1200/list-existing-databases-on-a-tabular-server-analysis-services-amo-tom.md)
