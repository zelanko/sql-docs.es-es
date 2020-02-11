---
title: Página de propiedades parámetros (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: ebb53598-2378-46ae-8935-d5192f8ea49a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 866fe023ff6ca2fe83264d65319618c5def0749a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108119"
---
# <a name="parameters-properties-page-report-manager"></a>Parámetros (página de propiedades del Administrador de informes)
  Utilice la página de propiedades Parámetros para ver o modificar la configuración de los parámetros de un informe con parámetros.  
  
 Los parámetros se especifican en la definición del informe antes de que se publique. Una vez publicado, se pueden modificar algunos valores de propiedades de parámetros. Los valores que se pueden modificar varían en función de cómo se hayan definido los parámetros en el informe. Por ejemplo, si se ha definido una lista de valores estáticos para un parámetro, se puede elegir un valor estático diferente para utilizarlo como valor predeterminado, pero no se pueden agregar ni quitar valores de la lista. De forma similar, si el parámetro se basa en una consulta, todos los aspectos de dicha consulta (por ejemplo, el conjunto de datos empleado, si se permiten valores NULL o en blanco, y si se suministra un valor predeterminado) se definen en el informe antes de su publicación.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-parameters-properties-page"></a>Para abrir la página de propiedades de parámetros  
  
1.  Abra el Administrador de informes y busque el informe para el que desea modificar la configuración de parámetros.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades General correspondiente al informe.  
  
4.  Seleccione la pestaña **parámetros** . Si la pestaña **parámetros** no está visible, el informe no contiene parámetros.  
  
## <a name="options"></a>Opciones  
 **Nombre del parámetro**  
 Especifica el nombre del parámetro.  
  
 **Tipo de datos**  
 Especifica el tipo de datos del parámetro.  
  
 **Tiene un valor predeterminado**  
 Active esta casilla para especificar si el parámetro tiene un valor predeterminado. Al activar esta casilla, se habilita la opción **Valor predeterminado**. También habilita **NULL** si el parámetro de informe acepta valores nulos. Si **Tiene un valor predeterminado** no está seleccionado, debe ocultar el valor o solicitarle al usuario que proporcione un valor cuando se ejecute el informe.  
  
 **Valor predeterminado**  
 Especifique un valor para el parámetro. Para especificar un valor predeterminado, debe activar la casilla **Tiene un valor predeterminado** y desactivar **NULL** . Puede proporcionar un valor predeterminado en la definición del informe. Si establece uno o varios valores estáticos para **Valor predeterminado** , esos valores se originan con el informe. Si **Valor predeterminado** es **Basado en consultas**, el valor del parámetro está determinado por una consulta definida en el informe.  
  
 Si **Valor predeterminado** acepta un valor, puede escribir una constante o sintaxis que sea válida para la extensión de procesamiento de datos utilizada con el informe. Por ejemplo, si el lenguaje de consultas de la extensión de procesamiento de datos admite caracteres comodín, puede especificar un comodín como valor predeterminado.  
  
 Si después especifica que se pregunte al usuario, el valor predeterminado se convierte en un valor inicial que los usuarios pueden utilizar o modificar. Si no se pide un valor de parámetro, se utiliza este valor para todos los usuarios que ejecuten el informe.  
  
 **Null**  
 Active esta casilla para especificar Null como valor predeterminado. Un valor Null implica que el informe se ejecuta incluso aunque el usuario no proporcione un valor de parámetro. Si no hay ninguna casilla en esta columna, el parámetro no acepta valores Null.  
  
 **Ocultar**  
 Active esta casilla para ocultar el parámetro en el área de parámetros que aparece en la parte superior del informe. El parámetro seguirá apareciendo en las páginas de definición de suscripciones y todavía se podrá especificar en una dirección URL de informe. Ocultar el parámetro resulta útil si se desea que el informe se ejecute siempre con un valor predeterminado que especifique.  
  
 Desactive la casilla si desea que el parámetro esté visible en el informe.  
  
 **Preguntar al usuario**  
 Active esta casilla para mostrar un cuadro de texto donde se pida a los usuarios un valor de parámetro.  
  
 Desactive esta casilla si desea ejecutar el informe en modo desatendido (por ejemplo, para generar un historial de informe o instantáneas de ejecución de informes), si desea usar el mismo valor de parámetro para todos los usuarios o si no es necesario que el usuario especifique el valor.  
  
 **Mostrar texto**  
 Escriba la cadena de texto que desea que aparezca junto al cuadro de texto del parámetro. Esta cadena proporciona una etiqueta o texto descriptivo. No hay límite para la longitud de la cadena. Las cadenas de texto más largas se ajustan al espacio proporcionado.  
  
## <a name="see-also"></a>Consulte también  
 [Página de propiedades generales, informes &#40;Administrador de informes&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
