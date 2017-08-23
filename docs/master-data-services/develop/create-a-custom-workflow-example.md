---
title: Ejemplo de flujo de trabajo personalizado (Master Data Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: dfd1616c-a75c-4f32-bdb1-7569e367bf41
caps.latest.revision: 6
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e2b3ad5ab349456364d2aa0af8826dd6970e55b1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="create-a-custom-workflow---example"></a>Ejemplo de creación de un flujo de trabajo personalizado:
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], cuando se crea una biblioteca de clases de flujo de trabajo personalizado, cree una clase que implementa la interfaz Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender. Esta interfaz incluye un método, <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A>, al que el servicio de integración de flujos de trabajo MDS de SQL Server llama cuando se inicia un flujo de trabajo. El <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> método contiene dos parámetros: *workflowType* contiene el texto que escribió en el **tipo de flujo de trabajo** cuadro de texto [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], y *elemento dataElement* contiene datos de elementos y metadatos para el elemento que desencadenó la regla de negocios de flujo de trabajo.  
  
## <a name="custom-workflow-example"></a>Ejemplo de flujo de trabajo personalizado  
 En el ejemplo de código siguiente se muestra cómo implementar el método <xref:Microsoft.MasterDataServices.WorkflowTypeExtender.IWorkflowTypeExtender.StartWorkflow%2A> para extraer los atributos Name, Code y LastChgUserName de los datos XML del elemento que desencadenó la regla de negocio del flujo de trabajo, y cómo llamar a un procedimiento almacenado para insertarlos en otra base de datos. Para obtener un ejemplo de los datos del elemento XML y una explicación de las etiquetas contiene, consulte [descripción de XML de flujo de trabajo personalizado &#40; Master Data Services &#41; ](../../master-data-services/develop/create-a-custom-workflow-xml-description.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Crear un flujo de trabajo personalizado &#40; Master Data Services &#41;](../../master-data-services/develop/create-a-custom-workflow-master-data-services.md)  
  
  
