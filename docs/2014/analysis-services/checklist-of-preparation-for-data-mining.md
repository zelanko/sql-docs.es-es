---
title: Lista de comprobación de preparación para la minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0e056c95-ba06-413e-8dc1-4d411a447c3b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c74fcbc925091a563d10bc8feef44337af48f84
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52519927"
---
# <a name="checklist-of-preparation-for-data-mining"></a>Lista de comprobación de la preparación para la minería de datos
  Pese a que los complementos de minería de datos facilitan y hacen más agradable la creación de modelos y la experimentación con los mismos, cuando se necesita obtener resultados repetibles y procesables, se debe prever un periodo adecuado para la formulación de requisitos de negocio básicos y para la obtención y preparación de los datos. En esta sección encontrará una lista de comprobación para ayudarle a planear la investigación, así como descripciones de los problemas comunes.  
  
## <a name="checklist-of-data-preparation"></a>Lista de comprobación para la preparación de datos  
 **He identificado un resultado claramente definido.**  
 Prepare un plan sobre el modo en que utilizará los resultados. Cada tipo de modelo tiene su propia salida. Un modelo de serie temporal genera los valores de una serie en el futuro, que pueden entenderse y procesarse fácilmente. Otros modelos generan conjuntos complejos que deben analizar los expertos en la materia para producir el máximo valor.  
  
-   ¿Qué salida desea?  
  
-   ¿Puede definir salida como una sola columna o valor, u otro resultado procesable?  
  
-   ¿Cuáles son los criterios para saber que el modelo fue útil?  
  
-   ¿Cómo utilizará e interpretará los resultados?  
  
-   ¿Puede asignar datos de entrada nuevos a los resultados esperados?  
  
 **Sé el significado y tipos de datos de distribución de los datos de entrada.**  
 Tómese un tiempo para explorar y comprender los datos de origen. Es importante que las personas que revisen el modelo conozcan el tipo de datos de entrada que se usaron y sepan cómo interpretar los tipos de datos y la variabilidad, así como el equilibrio y la calidad.  
  
-   ¿Cuántos datos tiene? ¿Hay suficientes datos para el modelado?  
  
     No tiene que ser una cantidad enorme - más pequeña y equilibrada puede ser aún mejor.  
  
-   ¿Proceden los datos de varios orígenes, o de uno solo?  
  
-   ¿Están los datos ya procesados y limpios? ¿Hay más datos de entrada disponibles?  
  
-   ¿Sabe cómo se ha manipulado antes de que haya recibido - cómo datos es posible que se han truncado, resumidos o convertir?  
  
-   ¿Tienen los datos de entrada algunos resultados de ejemplo que se pueden utilizar para el entrenamiento?  
  
 **Entiendo el nivel de integridad de los datos que tenemos y el nivel que necesitamos.**  
 Los datos incorrectos pueden afectar a la calidad del modelo, o impedir que este se genere. Debe contar con un buen conocimiento de la distribución y del significado de los datos, y saber cómo llegaron a este estado. Deberá entender si es posible o adecuado simplificar los datos mediante etiquetado, truncamiento de tipos de datos numéricos o resumen.  
  
-   Etiquetas de datos: ¿son claras y correctas?  
  
-   Tipos de datos: ¿son apropiados y se han modificado?  
  
-   ¿Ha ordenado, limpiado o descartado datos incorrectos?  
  
     ¿Ha comprobado que no haya duplicados?  
  
-   ¿Cómo trataría las situaciones donde faltan valores? ¿Qué indica la falta de valores?  
  
-   ¿Ha comprobado los orígenes para ver si se han podido introducir errores durante el proceso de importación?  
  
     ¿Dónde está almacenada la entrada? ¿Cuánto tiempo estará disponible?  
  
     ¿Existe un diccionario de datos? ¿Puede crear uno?  
  
-   ¿Si combinó conjuntos de datos, comprobó si había varias columnas que representaban los mismos datos?  
  
 **Sé donde se almacenan los datos de origen, de dónde proceden y cómo se procesan. El proceso puede repetirse fácilmente si es necesario.**  
 Conjuntos de datos únicos están bien para los experimentos, pero si desea mover el modelo en producción, conviene pensar de antemano en cómo se puede aplicar el proceso de limpieza a los datos operativos. Además, si tiene datos operativos, debe saber cómo se pueden haber sido modificado antes de que lo tienes-necesitará saber cómo se redondearon o resumido, sin duda.  
  
-   ¿Desea poder repetir el experimento?  
  
-   ¿Qué herramientas utilizaría para preparar datos en un formato que admita el análisis de datos? ¿Se pueden automatizar las operaciones de revisión y limpieza o se necesita a alguien para realizarlas en Excel?  
  
-   Si los datos proceden de otro sistema, ¿podrá capturar y hacer el seguimiento de los filtros que se aplicaron?  
  
-   ¿Puede aplicar también el marco de procesamiento de datos algoritmos de aprendizaje automático, realizar pruebas y visualizar resultados?  
  
 **Ha habido en la granularidad deseada de predicciones y nuestros datos se ha modificado para generar esas unidades.**  
 Antes de preparar los datos, debe decidir cuál va a ser la granularidad de los resultados. Por ejemplo, debe indicar si desea que los pronósticos de ventas sean por día o por trimestre. Puede considerar la posibilidad de configurar diferentes estructuras de datos para los mismos datos con objeto de controlar distintos niveles de resumen.  
  
-   ¿Cuál es la unidad de medida o la unidad de tiempo actual?  
  
     ¿Qué unidad desea usar en los resultados?  
  
-   ¿Es posible definir una unidad básica (por ejemplo, día / hora / min / llamada instruction) para todos los datos de entrada?  
  
     ¿Desea resumirlos en unidades de mayor nivel?  
  
-   ¿Están etiquetadas las categorías de forma coherente? ¿Es fácil agregar o quitar categorías?  
  
 **Nuestro diseño experimental es repetible y reproducible.**  
 Considere las estrategias para analizar y validar los resultados y cree un plan para capturar una instantánea de los datos que le permitirá asegurarse de que puede correlacionar los efectos con los datos. Si utiliza un valor de inicialización aleatorio, los resultados pueden diferir ligeramente. Esto puede dificultar la comparación y validación de modelos.  
  
-   ¿Si realiza muchos cambios personalizados en los datos, qué sucede la próxima vez desea generar el modelo?  
  
-   ¿Se ha definido previamente un procedimiento manual o un proceso aprobado que se debe usar para procesar la entrada y obtener los resultados deseados?  
  
-   ¿Ha decidido usar un valor de inicialización para el modelo?  
  
 **Se tiene conocimiento del dominio para validar los resultados, o tener acceso a expertos en el tema que nos pueden aconsejar.**  
 Emplee tiempo en validar las variables, el modelo y los resultados. Pida ayuda a los expertos para evaluar las interacciones y los resultados. Sin embargo, no permita que las suposiciones se impongan a la evidencia. Esté abierto a los hallazgos nuevos e inesperados.  
  
-   ¿Existe conocimiento del dominio disponible para ayudar a filtrar los datos y a reducir el ruido en la entrada?  
  
-   ¿Pueden los expertos del dominio ayudar a interpretar los resultados y sugerir mejoras?  
  
## <a name="see-also"></a>Vea también  
 [Elegir datos para minería de datos](choosing-data-for-data-mining.md)  
  
  
