---
title: Crear conjunto de pruebas (Asistente para minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.holdout.f1
ms.assetid: d0a44b59-ffbd-45fc-baa8-6b8046b1a2f5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 84dd9e307279c83b955d6569571772414123f0f5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84526491"
---
# <a name="create-testing-set-data-mining-wizard"></a>Crear conjunto de pruebas (Asistente para minería de datos)
  Utilice la página **Crear conjunto de pruebas** para especificar qué cantidad de datos se va a utilizar para el entrenamiento y cuánta se va a reservar para utilizarla en un conjunto de pruebas. Al separar los datos en un conjunto de aprendizaje y de pruebas cuando se crea una estructura de minería de datos, resulta más fácil evaluar la exactitud de los modelos de minería que se crean después.  
  
 Puede especificar la cantidad de datos de prueba como un porcentaje o puede especificar un número para limitar el número de casos que se utilizan para pruebas. Si especifica un porcentaje y un número máximo de casos que puedan utilizarse en pruebas, se utilizan ambas configuraciones y el conjunto de datos de pruebas contiene el número menor de casos. De forma predeterminada, el 30 por ciento de los datos se utiliza para pruebas, el 70 por ciento para aprendizaje y no hay ningún número máximo de casos de prueba.  
  
 De manera predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] genera un valor de inicialización numérico que se usa para iniciar las particiones. Este valor de inicialización está basado en el nombre de la estructura de minería de datos. Si desea asegurarse de que la partición se queda igual incluso si se cambia el nombre de la estructura de minería de datos, puede especificar un valor de inicialización si establece la propiedad HoldoutSeed de la estructura de minería de datos. Si cambia el valor de inicialización de la exclusión, debe volver a procesar la estructura.  
  
 Si posteriormente desea cambiar la cantidad de datos de prueba o de entrenamiento, puede modificar las `HoldoutMaxCases` propiedades y `HoldoutMaxPercent` en la estructura de minería de datos mediante la ventana **propiedades** . Sin embargo, después de realizar la modificación debe volver a procesar la estructura de minería de datos y todos los modelos de minería asociados. También se aplican las siguientes limitaciones:  
  
-   El particionamiento de una estructura de minería de datos solamente se admite cuando la estructura está almacenada en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Las versiones anteriores de no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admiten el almacenamiento en caché de la información de particiones para estructuras de minería de datos.  
  
-   No se puede dividir una estructura de minería de datos si ésta contiene una columna de clave temporal, que se requiere para los modelos de minería de datos de serie temporal.  
  
-   No se pueden dividir los datos si está intentando predecir un valor que está almacenado en una tabla anidada.  
  
 **Para más información:** [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md), [Crear una estructura de min6ería de datos relacional](data-mining/create-a-relational-mining-structure.md), [Tutorial básico de minería de datos](../../2014/tutorials/basic-data-mining-tutorial.md)  
  
## <a name="options"></a>Opciones  
 **Porcentaje de datos para pruebas**  
 Haga clic en las flechas arriba y abajo para aumentar o disminuir el porcentaje de datos que se van a utilizar como un conjunto de aprendizaje o escriba un valor entre 0 y 100 en el cuadro de texto.  
  
 **Número máximo de casos para el conjunto de datos de prueba**  
 Escriba un número para limitar el número de casos que se pueden utilizar para realizar las pruebas.  
  
 Si especifica un número mayor que el número de casos reales en los datos, se utilizarán todos los casos.  
  
 El valor predeterminado es NULL. Esto significa que no hay ningún límite.  
  
## <a name="see-also"></a>Consulte también  
 [Asistente para minería de datos (ayuda F1) &#40;Analysis Services: minería de datos&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Sugerir columnas relacionadas &#40;Asistente para minería de datos&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Especificar tipos de tablas &#40;Asistente para minería de datos&#41;](specify-table-types-data-mining-wizard.md)   
 [Especifique el contenido y el tipo de datos de la columna &#40;Asistente para minería de datos&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
