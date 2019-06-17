---
title: 'Tarea 1: Crear una Base de conocimiento y dominios | Microsoft Docs'
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 7d74a60b-8933-4038-bcbb-4e9dcc4f70e9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 79edd8566f2b3c9b586bc8c8815e1d9bc586fb05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481242"
---
# <a name="task-1-creating-a-knowledge-base-and-domains"></a>Tarea 1: Creación de una base de conocimiento y dominios
  En esta tarea, creará el **proveedores** base de conocimiento y creará dominios que se usa para la limpieza y coincidencia de datos para quitar duplicados.  
  
1.  Iniciar **Data Quality Client**. Haga clic en **iniciar**, apunte a **todos los programas**, haga clic en **Microsoft SQL Server 2012**, haga clic en **Data Quality Services**y, a continuación, haga clic en  **Data Quality Client**.  
  
2.  En el **conectar al servidor** cuadro de diálogo, seleccione la instancia del servidor de base de datos en el que está instalado DQS y haga clic en **Connect**.  
  
     ![Conectar con el cuadro de diálogo servidor](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-01.jpg "conectarse al cuadro de diálogo de servidor")  
  
3.  En el cliente de calidad de datos de página principal, en el **administración de la Base de conocimiento** panel, haga clic en **nueva Base de conocimiento**.  
  
     ![Administración de la Base de conocimiento - nueva KB](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-02.jpg "administración de la Base de conocimiento - nueva KB")  
  
4.  Escriba **proveedores** para **nombre** de la base de conocimiento.  
  
     ![Nueva Base de conocimiento - administración de dominios](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-03.jpg "nueva Knowledge Base - administración de dominios")  
  
5.  Confirme que **crear Base de conocimiento desde** campo se establece en **ninguno** puesto que está creando el **proveedores** base de conocimiento desde cero.  
  
6.  Confirme que **Domain Management** está seleccionada para la **actividad** y haga clic en **siguiente**. La actividad Administración de dominios permite crear y administrar dominios en la base de conocimiento.  
  
7.  En el **Domain Management** ventana, haga clic en **crear un dominio** botón de barra de herramientas para crear un dominio.  
  
     ![Crear el botón de barra de herramientas de dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-04.jpg "crear el botón de barra de herramientas de dominio")  
  
8.  En el **crear dominio** cuadro de diálogo, escriba **Id. de proveedor** para el **nombre de dominio**y haga clic en **Aceptar**.  
  
     ![Crear el cuadro de diálogo dominio](../../2014/tutorials/media/et-creatingaknowledgebaseanddomains-05.jpg "crear el cuadro de diálogo dominio")  
  
9. Repita el paso anterior para crear los dominios siguientes con toda la configuración predeterminada. Para simplificar el tutorial, configuró el **tipo de datos** de todos los dominios como **cadena**. Los otros tipos de datos permitidos son: Entero, Decimal y fecha. Cuando el **usar valores iniciales** opción está activada (valor predeterminado), todos los sinónimos se reemplazan con el valor inicial del grupo de sinónimos en la salida. Establecer **normalizar cadena** (valor predeterminado) quita todos los caracteres especiales en los valores de dominio. El **formato de salida para** opción le permite seleccionar el formato que se aplica cuando los valores de los datos en el dominio. Seleccione **Habilitar corrector ortográfico** (valor predeterminado) para ejecutar el corrector ortográfico en todos los valores de cadena al rellenar el dominio. El **lenguaje** configuración especifica la versión de idioma de la **corrector ortográfico** que desea aplicar. Seleccione **deshabilitar algoritmos de Error de sintaxis** para rellenar el dominio sin comprobar los valores de cadena para errores de sintaxis. Consulte [crear un dominio](https://msdn.microsoft.com/library/hh510401.aspx) tema en MSDN library para obtener más detalles.  
  
    -   Nombre de proveedor  
  
    -   Póngase en contacto con el correo electrónico  
  
    -   Address Line  
  
    -   City  
  
    -   State  
  
    -   País  
  
    -   Zip  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 2: Agregar manualmente los valores de dominio](../../2014/tutorials/task-2-adding-domain-values-manually.md)  
  
  
