---
title: Definir asignaciones y otros comandos de Script | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 024a70622607b3c40af491320085199c921f23fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="define-assignments-and-other-script-commands"></a>Definir asignaciones y otros comandos de script
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En la pestaña **Cálculos** del Diseñador de cubos, haga clic en el icono **Nuevo comando de script** de la barra de herramientas para crear un script vacío. Cuando cree un script, aparecerá inicialmente con un título en blanco en el panel **Organizador de script** de la pestaña Cálculos. Los caracteres escritos en el panel de las expresiones de cálculo estarán visibles como nombre del elemento en **Organizador de script**. Por lo tanto, puede que desee escribir un nombre comentado en la primera línea para identificar más fácilmente el script en el panel **Organizador de script** . Para obtener más información, vea la [introducción a scripting de MDX en Microsoft SQL Server 2005](http://go.microsoft.com/fwlink/?LinkId=81892). Para obtener más información acerca de los problemas de rendimiento relacionados con las consultas y cálculos de MDX, vea la sección sobre escritura de MDX eficaz en la [guía de rendimiento de SQL Server 2005 Analysis Services](http://go.microsoft.com/fwlink/?LinkId=81621).  
  
> [!IMPORTANT]  
>  Cuando cambie inicialmente a la pestaña **Cálculos** del Diseñador de cubos, el panel **Organizador de script** contendrá un único script con un comando CALCULATE. El comando CALCULATE controla la agregación de las celdas en el cubo y solo debería editarse si se desea especificar manualmente la forma en que se debería agregar el cubo.  
  
 Puede utilizar el panel de las expresiones de cálculo para generar una expresión con la sintaxis MDX (Expresiones multidimensionales). Mientras genera la expresión, puede arrastrar o copiar los componentes, las funciones y las plantillas del cubo del panel **Herramientas de cálculo** al panel de las expresiones de cálculo. De esta forma se agregará el script para el elemento al panel de las expresiones de cálculo en la ubicación, en la que la coloque o pegue. Reemplace los argumentos y sus delimitadores (« y ») con los valores correspondientes.  
  
> [!IMPORTANT]  
>  Cuando escriba una expresión que contenga varias instrucciones mediante el panel de las expresiones de cálculo, asegúrese de que todas las líneas salvo la última del script MDX finalicen por un punto y coma (;). Los cálculos se concatenan en un único script MDX, y cada script tiene un punto y coma anexado a ella para asegurarse de que el script MDX se compila correctamente. Si agrega un punto y coma a la última línea del script del panel de las expresiones de cálculo, el cubo se generará e implementará correctamente, pero no podrá ejecutar consultas en él.  
  
## <a name="see-also"></a>Vea también  
 [Cálculos en modelos multidimensionales](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
