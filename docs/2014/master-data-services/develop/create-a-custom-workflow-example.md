---
title: Ejemplo de flujo de trabajo personalizado (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 9d72e31b8e4040353c9c93bceb65ca3c2be98788
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469050"
---
# <a name="custom-workflow-example-master-data-services"></a>Ejemplo de flujo de trabajo personalizado (Master Data Services)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] , cuando se crea una biblioteca de clases de flujo de trabajo personalizada, se crea una clase que implementa la interfaz [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender](/previous-versions/sql/sql-server-2016/hh758785(v=sql.130)) . Esta interfaz incluye un método, [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)), al que llama SQL Server servicio de integración de flujos de trabajo de MDS cuando se inicia un flujo de trabajo. El método [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) contiene dos parámetros: *workflowType* contiene el texto que escribió en el cuadro de texto **tipo de flujo de trabajo** en [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , y el *elemento* DataItem contiene metadatos y datos de elementos para el elemento que desencadenó la regla de negocio del flujo de trabajo.  
  
## <a name="custom-workflow-example"></a>Ejemplo de flujo de trabajo personalizado  
 En el ejemplo de código siguiente se muestra cómo implementar el método [Microsoft. MasterDataServices. WorkflowTypeExtender. IWorkflowTypeExtender. StartWorkflow *](/previous-versions/sql/sql-server-2016/hh759009(v=sql.130)) para extraer el nombre, el código y los atributos de LastChgUserName de los datos XML para el elemento que desencadenó la regla de negocio del flujo de trabajo y cómo llamar a un procedimiento almacenado para insertarlos en otra base de datos. Para ver un ejemplo del código XML de datos de elementos y una explicación de las etiquetas que este contiene, vea [Descripción del código XML de flujo de trabajo personalizado &#40;Master Data Services&#41;](create-a-custom-workflow-xml-description.md).  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.IO;  
using System.Data.SqlClient;  
using System.Xml;  
  
using Microsoft.MasterDataServices.Core.Workflow;  
  
namespace MDSWorkflowTestLib  
{  
    public class WorkflowTester : IWorkflowTypeExtender  
    {  
        #region IWorkflowTypeExtender Members  
  
        public void StartWorkflow(string workflowType, System.Xml.XmlElement dataElement)  
        {  
            // Extract the attributes we want out of the element data.  
            XmlNode NameNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Name");  
            XmlNode CodeNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/Code");  
            XmlNode EnteringUserNode = dataElement.SelectSingleNode("//ExternalAction/MemberData/LastChgUserName");  
  
            // Open a connection on the workflow database.  
            SqlConnection workflowConn = new SqlConnection(@"Data Source=<Server instance>; Initial Catalog=WorkflowTest; Integrated Security=True");  
  
            // Create a command to call the stored procedure that adds a new user to the workflow database.  
            SqlCommand addCustomerCommand = new SqlCommand("AddNewCustomer", workflowConn);  
            addCustomerCommand.CommandType = System.Data.CommandType.StoredProcedure;  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Name", NameNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@Code", CodeNode.InnerText));  
            addCustomerCommand.Parameters.Add(new SqlParameter("@EnteringUser", EnteringUserNode.InnerText));  
  
            // Execute the command.  
            workflowConn.Open();  
            addCustomerCommand.ExecuteNonQuery();  
            workflowConn.Close();  
        }  
  
        #endregion  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Crear un flujo de trabajo personalizado &#40;Master Data Services&#41;](create-a-custom-workflow-master-data-services.md)  
  
  
