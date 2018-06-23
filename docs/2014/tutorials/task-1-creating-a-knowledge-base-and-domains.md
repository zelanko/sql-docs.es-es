---
title: 'Tarea 1: Crear una Base de conocimiento y dominios | Documentos de Microsoft'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: beec636f9137802c6651f0c08889acf73000b063
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198778"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>TArea 1: crear una base de conocimiento y dominios
  En esta tarea, creará el **proveedores** base de conocimiento y crear dominios que se usa para la limpieza y coincidencia de datos para quitar duplicados.  
  
1.  Iniciar **Data Quality Client**. Haga clic en **iniciar**, seleccione **todos los programas**, haga clic en **Microsoft SQL Server 2012**, haga clic en **Data Quality Services**y, a continuación, haga clic en  **Cliente de calidad de datos**.  
  
2.  En el **conectar al servidor** diálogo cuadro, seleccione la instancia de servidor de base de datos en el que está instalado DQS y haga clic en **conectar**.  
  
     ![Conectarse al servidor, cuadro de diálogo](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "conectarse al servidor, cuadro de diálogo")  
  
3.  En el cliente de calidad de datos página principal, en la **administración de la Base de conocimiento** panel, haga clic en **nueva Base de conocimiento**.  
  
     ![Administración de la Base de conocimiento - nueva KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "administración de la Base de conocimiento - nueva KB")  
  
4.  Escriba **proveedores** para **nombre** de la base de conocimiento.  
  
     ![Nueva Base de conocimiento - administración de dominios](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "nueva Knowledge Base - administración de dominios")  
  
5.  Confirme que **crear la Base de conocimiento desde** campo está establecido en **ninguno** porque va a crear la **proveedores** base de conocimiento desde cero.  
  
6.  Confirme que **Domain Management** está seleccionada para la **actividad** y haga clic en **siguiente**. La actividad Administración de dominios permite crear y administrar dominios en la base de conocimiento.  
  
7.  En el **Domain Management** ventana, haga clic en **crear un dominio** botón de barra de herramientas para crear un dominio.  
  
     ![Crear el botón de barra de herramientas de dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "Crear botón de barra de herramientas de dominio")  
  
8.  En el **crear dominio** cuadro de diálogo, escriba **Id. de proveedor** para el **nombre de dominio**y haga clic en **Aceptar**.  
  
     ![Crear cuadro de diálogo dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "Crear cuadro de diálogo dominio")  
  
9. Repita el paso anterior para crear los dominios siguientes con toda la configuración predeterminada. Para simplificar el tutorial, establezca la **tipo de datos** de todos los dominios como **cadena**. Los otros tipos de datos permitidos son: Integer, Decimal y Date. Cuando el **usar valores iniciales** opción está activada (valor predeterminado), todos los sinónimos se reemplazan con el valor inicial del grupo de sinónimos en el resultado. Establecer **normalizar cadena** (valor predeterminado), quita todos los caracteres especiales en los valores de dominio. El **dar formato al resultado para** opción le permite seleccionar el formato que se aplica cuando se generen los valores de datos en el dominio. Seleccione **Habilitar corrector ortográfico** (valor predeterminado) para ejecutar el corrector ortográfico en todos los valores de cadena al rellenar el dominio. El **lenguaje** configuración especifica la versión de idioma de la **corrector ortográfico** que desea aplicar. Seleccione **deshabilitar algoritmos de Error de sintaxis** para rellenar el dominio sin comprobar errores de sintaxis de los valores de cadena. Vea [crear un dominio](http://msdn.microsoft.com/library/hh510401.aspx) tema en MSDN library para obtener más detalles.  
  
    -   Nombre de proveedor  
  
    -   Póngase en contacto con el correo electrónico  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   País  
  
    -   Zip  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 2: Agregar valores de dominio manualmente](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  