---
title: "Decision"
url: /studio7/microflows-decision/
category: "Microflows"
weight: 20
description: "Describes a decision in Mendix Studio."
tags: ["studio", "microflow", "exclusive split", "decision"]
---

## 1 Introduction 

This document describes a **Decision** in Mendix Studio. 

A decision is an element based on a condition and follows one and only one of the outgoing flows. For example, you need to use a decision to show different order forms for the customers with different grades, or to prevent a blocked customer from making orders.

## 2 Condition

There are two ways to configure a condition for the decision:

* [With **Variables/ Attributes**](#variables-attributes-tab) ( for example, you can use it to create different flows for an attribute of the enumeration type)
* [With an **Expression**](#expression-tab) (for example, you can create a comparison with it)

    {{< figure src="/attachments/studio7/microflows/microflows-decision/configure-condition-dialog.png" >}}

### 2.1 Configuring the Condition with Variables or Attributes {#variables-attributes-tab}

The following elements can be used as a decision condition in the **Variable/Attributes** tab:

* Variable with Boolean data type
* Variable with enumeration data type
* Attribute  of Boolean type
* Attribute of enumeration type

{{% alert color="info" %}}
The parameters and entities which you would like to use in configuring the condition of the decision should be present in the microflow, either as input parameter or as a result of an activity. 
{{% /alert %}}

### 2.2 Configuring the Condition with an Expression {#expression-tab}

You can also configure the condition by writing the expression. For more information, see [Microflow Expressions](/studio7/microflows-expressions/).

## 3 Cases

The number of available cases depends on the selected **Condition**. 

For the Boolean type of the parameter or attribute, two values are possible: true and false.  

{{< figure src="/attachments/studio7/microflows/microflows-decision/decision-boolean.png" >}}

The number of cases available for the enumeration type depends on the corresponding enumeration constants/values. There is also the empty case available for enumeration. If the enumeration parameter or attribute of an object is unassigned, the sequence flow with the caption (empty) is followed.

{{< figure src="/attachments/studio7/microflows/microflows-decision/decision-enumeration.png" >}}

## 4 Caption

The caption describes what happens in this element.

## 5 Read More

* [Microflows](/studio7/microflows/)
* [Microflow Expressions](/studio7/microflows-expressions/)
* [Configure a  Decision](/studio7/microflows-how-to-configure-decision/) 
