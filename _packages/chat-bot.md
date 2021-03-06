---
title: Chat Bot
excerpt: A preconfigured bot with some helpful text-based conversational interactions.
layout: integration
topic: Packages
permalink: /packages/chat-bot/
redirect_from:
  - /guides/bots/conversational-bots/
jumbotron:
  title: Chat Bot
  tagline: ""
  breadcrumbs:
  -
    label: Resources &raquo;
    url: /resources/
  -
    label: Packages &raquo;
    url: /resources/packages/
---

* TOC
{:toc}

# Introduction

<iframe src="https://player.vimeo.com/video/223537123" width="880" height="495" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

This package adds a preconfigured [bot](/docs/bots/) with some helpful text-based conversational interactions.

Conversational computing[^chatbot] is a shift toward talking with software using natural language in order to retrieve information and accomplish tasks, rather than pointing and clicking through complex graphical user interfaces.

For instance, these are the steps that have been required to perform a simple search in Cerb (and it's not much different for most other apps):

1. Open your web browser
1. Navigate to a specific URL
1. Move your mouse to a menu and click it
1. Click on a link in the menu
1. Move the cursor to a text box somewhere and click it
1. Type some text to search for
1. Add some filters (much more reading, clicking, and typing)
1. Click a button to start the search
1. Get some results back (finally)
1. Sort, subtotal, and/or paginate the results

That's a very mechanical process -- and you probably do it at least a few dozen times per day.

With conversational computing, you could simply say (or type):

`find open tickets from Ghoux Games since last Monday`

Your chat bot says, _"Here's what I found"_, and a [worklist](/docs/workspaces/#worklists) instantly popups up with exactly what you're looking for. 

A few years ago that would have still been in the realm of science fiction.  Today you probably already converse with virtual personal assistants[^ipa] like Alexa, Siri, Cortana, or Google Assistant.

Conversational bots in Cerb provide you with the same conveniences as those assistants, but with the complete freedom to build new behaviors and add new abilities, to integrate with other services, and to take advantage of all the data you already have in Cerb.  Our bots know who you and your clients are, contact information and organizational relationships, the conversations you've had, open tasks, unread notifications, and so on.

You may have already automated many of your business processes using Cerb bot behaviors.  Let's explore how conversational behaviors can save your workers even more time.

# Installing the package

Navigate to **Setup >> Configure >> Import Package**.

Paste the following package into the large text box:

<pre style="max-height: 29.25em;">
<code class="language-json">
{% raw %}
{
  "package": {
    "name": "Chat Bot",
    "cerb_version": "8.0.1",
    "revision": 1,
    "requires": {
      "cerb_version": "8.0.1",
      "plugins": [

      ]
    },
    "configure": {
      "prompts": [

      ],
      "placeholders": [

      ]
    }
  },
  "bots": [
    {
      "uid": "bot_6",
      "name": "Cerb",
      "owner": {
        "context": "cerberusweb.contexts.app",
        "id": 0
      },
      "is_disabled": false,
      "params": {
        "config": null,
        "events": {
          "mode": "all",
          "items": [

          ]
        },
        "actions": {
          "mode": "all",
          "items": [

          ]
        }
      },
      "image": "data:image/png;base64,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",
      "behaviors": [
        {
          "uid": "behavior_28",
          "title": "Get interactions for worker",
          "is_disabled": false,
          "is_private": false,
          "priority": 1,
          "event": {
            "key": "event.interactions.get.worker",
            "label": "Conversation get interactions for worker",
            "params": {
              "listen_points": "global\r\n"
            }
          },
          "nodes": [
            {
              "type": "switch",
              "title": "Interaction:",
              "status": "live",
              "nodes": [
                {
                  "type": "outcome",
                  "title": "global",
                  "status": "live",
                  "params": {
                    "groups": [
                      {
                        "any": 0,
                        "conditions": [
                          {
                            "condition": "point",
                            "oper": "is",
                            "value": "global"
                          }
                        ]
                      }
                    ]
                  },
                  "nodes": [
                    {
                      "type": "action",
                      "title": "Return interactions",
                      "status": "live",
                      "params": {
                        "actions": [
                          {
                            "action": "return_interaction",
                            "behavior_id": "{{{uid.behavior_29}}}",
                            "name": "Start chat",
                            "interaction": "chat",
                            "interaction_params_json": ""
                          }
                        ]
                      }
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "uid": "behavior_29",
          "title": "Handle interaction with worker",
          "is_disabled": false,
          "is_private": false,
          "priority": 1,
          "event": {
            "key": "event.interaction.chat.worker",
            "label": "Conversation handle interaction with worker"
          },
          "nodes": [
            {
              "type": "switch",
              "title": "Interaction:",
              "status": "live",
              "nodes": [
                {
                  "type": "outcome",
                  "title": "chat",
                  "status": "live",
                  "params": {
                    "groups": [
                      {
                        "any": 0,
                        "conditions": [
                          {
                            "condition": "interaction",
                            "oper": "is",
                            "value": "chat"
                          }
                        ]
                      }
                    ]
                  },
                  "nodes": [
                    {
                      "type": "action",
                      "title": "Run behavior",
                      "status": "live",
                      "params": {
                        "actions": [
                          {
                            "action": "switch_behavior",
                            "return": "0",
                            "behavior_id": "{{{uid.behavior_27}}}",
                            "var": "_behavior"
                          }
                        ]
                      }
                    }
                  ]
                }
              ]
            }
          ]
        },
        {
          "uid": "behavior_27",
          "title": "Respond to worker chat",
          "is_disabled": false,
          "is_private": false,
          "priority": 1,
          "event": {
            "key": "event.message.chat.worker",
            "label": "Conversation with worker"
          },
          "nodes": [
            {
              "type": "action",
              "title": "Hi!",
              "status": "live",
              "params": {
                "actions": [
                  {
                    "action": "_set_custom_var",
                    "value": "Hi, {{worker_first_name}}. Say **help** for a list of things I can help you with.",
                    "format": "",
                    "is_simulator_only": "0",
                    "var": "say"
                  },
                  {
                    "action": "_run_subroutine",
                    "subroutine": "say()"
                  }
                ]
              }
            },
            {
              "type": "loop",
              "title": "Loop forever",
              "status": "live",
              "params": {
                "foreach_json": "[\"*\"]",
                "as_placeholder": "loops"
              },
              "nodes": [
                {
                  "type": "action",
                  "title": "Prompt",
                  "status": "live",
                  "params": {
                    "actions": [
                      {
                        "action": "prompt_text",
                        "placeholder": "say something, or type 'help'"
                      }
                    ]
                  }
                },
                {
                  "type": "action",
                  "title": "Detect intent from chat message with a classifier",
                  "status": "live",
                  "params": {
                    "actions": [
                      {
                        "action": "core.va.action.classifier_prediction",
                        "classifier_id": "{{{uid.classifier_001}}}",
                        "content": "{{message}}",
                        "object_placeholder": "_prediction"
                      }
                    ]
                  }
                },
                {
                  "type": "switch",
                  "title": "Intent:",
                  "status": "live",
                  "nodes": [
                    {
                      "type": "outcome",
                      "title": "(new conversation)",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "message",
                                "oper": "is",
                                "value": ""
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: Welcome",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "Hi, {{worker_first_name}}. Say **help** for a list of things I can help you with.",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "say.bye",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.classification.name}}",
                                "oper": "is",
                                "value": "say.bye"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: Bye!",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% set r = [\r\n\"bye \" ~ worker_first_name ~ \"!\",\r\n] %}\r\n{{random(r)}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              },
                              {
                                "action": "prompt_wait"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Close window",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "window_close"
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "say.hello",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.classification.name}}",
                                "oper": "is",
                                "value": "say.hello"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: Hello!",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% set r = [\r\n\"Hello \" ~ worker_first_name,\r\n\"Hi, \" ~ worker_first_name,\r\n\"Hi \" ~ worker_first_name,\r\n\"Howdy \" ~ worker_first_name,\r\n\"Hi there \" ~ worker_first_name,\r\n\"hey \" ~ worker_first_name,\r\n] %}\r\n{{random(r)}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "ask.help",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.classification.name}}",
                                "oper": "is",
                                "value": "ask.help"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: Help",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "Try one of these: \r\n- help\r\n- hi\r\n- What time is it?\r\n- find my open tickets\r\n- show waiting tickets from Jan 2015 to now\r\n- find Mara's messages from this year\r\n- search my open tasks\r\n- show my new notifications\r\n- bye",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "ask.time",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.classification.name}}",
                                "oper": "is",
                                "value": "ask.time"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: The time is...",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% set r = [\r\n\"It's \" ~ 'now'|date('g:i a'),\r\n\"The time is \" ~ 'now'|date('g:i a'),\r\n'now'|date('g:i a'),\r\n] %}\r\n{{random(r)}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "worklist.search",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.classification.name}}",
                                "oper": "is",
                                "value": "worklist.search"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearch()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearch()"
                              }
                            ]
                          }
                        }
                      ]
                    }
                  ]
                }
              ]
            },
            {
              "type": "subroutine",
              "title": "say()",
              "status": "live",
              "nodes": [
                {
                  "type": "action",
                  "title": "Respond in text",
                  "status": "live",
                  "params": {
                    "actions": [
                      {
                        "action": "send_message",
                        "message": "{{say}}",
                        "format": "markdown"
                      }
                    ]
                  }
                }
              ]
            },
            {
              "type": "subroutine",
              "title": "worklistSearch()",
              "status": "live",
              "nodes": [
                {
                  "type": "switch",
                  "title": "Context:",
                  "status": "live",
                  "nodes": [
                    {
                      "type": "outcome",
                      "title": "Tickets",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.params.context|keys|first}}",
                                "oper": "is",
                                "value": "cerberusweb.contexts.ticket"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearchConfirmation()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearchConfirmation()"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Open ticket worklist",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% spaceless %}\r\n{% set filters = [] %}\r\n{% set date = _prediction.params.date|first %}\r\n{% set org = _prediction.params.org|first|keys|first %}\r\n{% set owner = _prediction.params.worker|first|keys|first %}\r\n{% set status = _prediction.params.status|keys %}\r\n\r\n{% if owner is not empty %}\r\n  {% set filters = dict_set(filters, '[]', \"owner.id:\" ~ owner) %}\r\n{% endif %}\r\n\r\n{% if status is not empty %}\r\n  {% set filters = dict_set(filters, '[]', \"status:[\" ~ status|join(',') ~ \"]\") %}\r\n{% endif %}\r\n\r\n{% if org is not empty %}\r\n  {% set filters = dict_set(filters, '[]', \"org.id:\" ~ org) %}\r\n{% endif %}\r\n\r\n{% if date is not empty %}\r\n  {% set filters = dict_set(filters, '[]', 'updated:\"' ~ date.date ~ '\"') %}\r\n{% endif %}\r\n\r\n{% endspaceless %}\r\n{{filters|join(' ')}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "_query"
                              },
                              {
                                "action": "worklist_open",
                                "context": "cerberusweb.contexts.ticket",
                                "quick_search": "{{_query}}",
                                "worklist_model": null
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "Messages",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.params.context|keys|first}}",
                                "oper": "is",
                                "value": "cerberusweb.contexts.message"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearchConfirmation()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearchConfirmation()"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Open message worklist",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% spaceless %}\r\n{% set filters = [] %}\r\n{% set date = _prediction.params.date|first %}\r\n{% set worker = _prediction.params.worker|first|keys|first %}\r\n{% set status = _prediction.params.status|keys %}\r\n\r\n{% if worker is not empty %}\r\n  {% set filters = dict_set(filters, '[]', \"worker.id:\" ~ worker) %}\r\n{% endif %}\r\n\r\n{% if status is not empty %}\r\n  {% set filters = dict_set(filters, '[]', \"ticket:(status:[\" ~ status|join(',') ~ \"])\") %}\r\n{% endif %}\r\n\r\n{% if date is not empty %}\r\n  {% set filters = dict_set(filters, '[]', 'created:\"' ~ date.date ~ '\"') %}\r\n{% endif %}\r\n\r\n{% endspaceless %}\r\n{{filters|join(' ')}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "_query"
                              },
                              {
                                "action": "worklist_open",
                                "context": "cerberusweb.contexts.message",
                                "quick_search": "{{_query}}",
                                "worklist_model": null
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "Activity Logs",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.params.context|keys|first}}",
                                "oper": "is",
                                "value": "cerberusweb.contexts.activity_log"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearchConfirmation()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearchConfirmation()"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Open activity log worklist",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% spaceless %}\r\n{% set filters = [] %}\r\n{% set date = _prediction.params.date|first %}\r\n{% set owner = _prediction.params.worker|first|keys|first %}\r\n\r\n{% if owner is not empty %}\r\n{% set filters = dict_set(filters, '[]', \"actor.worker:(id:\" ~ owner ~ \")\") %}\r\n{% endif %}\r\n\r\n{% if date is not empty %}\r\n  {% set filters = dict_set(filters, '[]', 'created:\"' ~ date.date ~ '\"') %}\r\n{% endif %}\r\n\r\n{% endspaceless %}\r\n{{filters|join(' ')}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "_query"
                              },
                              {
                                "action": "worklist_open",
                                "context": "cerberusweb.contexts.activity_log",
                                "quick_search": "{{_query}}",
                                "worklist_model": null
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "Notifications",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.params.context|keys|first}}",
                                "oper": "is",
                                "value": "cerberusweb.contexts.notification"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearchConfirmation()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearchConfirmation()"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Open notification worklist",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% spaceless %}\r\n{% set filters = [] %}\r\n{% set status = _prediction.params.status|keys|first %}\r\n{% set owner = _prediction.params.worker|first|keys|first %}\r\n\r\n{% if owner is not empty %}\r\n{% set filters = dict_set(filters, '[]', \"worker.id:\" ~ owner) %}\r\n{% else %}\r\n{% set filters = dict_set(filters, '[]', \"worker:me\") %}\r\n{% endif %}\r\n\r\n{% if status is not empty and status == 'closed' %}\r\n  {% set filters = dict_set(filters, '[]', \"isRead:1\") %}\r\n{% else %}\r\n  {% set filters = dict_set(filters, '[]', \"isRead:0\") %}\r\n{% endif %}\r\n\r\n{% endspaceless %}\r\n{{filters|join(' ')}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "_query"
                              },
                              {
                                "action": "worklist_open",
                                "context": "cerberusweb.contexts.notification",
                                "quick_search": "{{_query}}",
                                "worklist_model": null
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "Tasks",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [
                              {
                                "condition": "_custom_script",
                                "tpl": "{{_prediction.params.context|keys|first}}",
                                "oper": "is",
                                "value": "cerberusweb.contexts.task"
                              }
                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "worklistSearchConfirmation()",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_run_subroutine",
                                "subroutine": "worklistSearchConfirmation()"
                              }
                            ]
                          }
                        },
                        {
                          "type": "action",
                          "title": "Open task worklist",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% spaceless %}\r\n{% set filters = [] %}\r\n{% set date = _prediction.params.date|first %}\r\n{% set status = _prediction.params.status|keys|first %}\r\n{% set owner = _prediction.params.worker|first|keys|first %}\r\n\r\n{% if owner is not empty %}\r\n{% set filters = dict_set(filters, '[]', \"owner.id:\" ~ owner) %}\r\n{% endif %}\r\n\r\n{% if status is not empty %}\r\n  {% if status == 'closed' %}\r\n  {% set filters = dict_set(filters, '[]', \"isCompleted:1\") %}\r\n  {% else %}\r\n  {% set filters = dict_set(filters, '[]', \"isCompleted:0\") %}\r\n  {% endif %}\r\n{% endif %}\r\n\r\n{% if date is not empty %}\r\n  {% set filters = dict_set(filters, '[]', 'due:\"big bang to ' ~ date.date ~ '\"') %}\r\n{% endif %}\r\n\r\n{% endspaceless %}\r\n{{filters|join(' ')}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "_query"
                              },
                              {
                                "action": "worklist_open",
                                "context": "cerberusweb.contexts.task",
                                "quick_search": "{{_query}}",
                                "worklist_model": null
                              }
                            ]
                          }
                        }
                      ]
                    },
                    {
                      "type": "outcome",
                      "title": "No",
                      "status": "live",
                      "params": {
                        "groups": [
                          {
                            "any": 0,
                            "conditions": [

                            ]
                          }
                        ]
                      },
                      "nodes": [
                        {
                          "type": "action",
                          "title": "Respond: Sorry...",
                          "status": "live",
                          "params": {
                            "actions": [
                              {
                                "action": "_set_custom_var",
                                "value": "{% set r = [\r\n\"Sorry, I'm not sure what you're looking for.\",\r\n\"Sorry, I'm not able to search \" ~ _prediction.params.context|first|default('for that') ~ \" yet.\",\r\n] %}\r\n{{random(r)}}",
                                "format": "",
                                "is_simulator_only": "0",
                                "var": "say"
                              },
                              {
                                "action": "_run_subroutine",
                                "subroutine": "say()"
                              }
                            ]
                          }
                        }
                      ]
                    }
                  ]
                }
              ]
            },
            {
              "type": "subroutine",
              "title": "worklistSearchConfirmation()",
              "status": "live",
              "nodes": [
                {
                  "type": "action",
                  "title": "Respond: I've found...",
                  "status": "live",
                  "params": {
                    "actions": [
                      {
                        "action": "_set_custom_var",
                        "value": "{% set r = [\r\n\"Certainly. Here you are.\",\r\n\"Certainly. I've located the records you're looking for.\",\r\n\"I've pulled up that worklist for you.\",\r\n\"I ran that search for you.\",\r\n] %}\r\n{{random(r)}}",
                        "format": "",
                        "is_simulator_only": "0",
                        "var": "say"
                      },
                      {
                        "action": "_run_subroutine",
                        "subroutine": "say()"
                      }
                    ]
                  }
                }
              ]
            }
          ]
        }
      ]
    }
  ],
  "classifiers": [
    {
      "uid": "classifier_001",
      "name": "Detect Intent",
      "owner": {
        "context": "cerberusweb.contexts.bot",
        "id": "{{{uid.bot_6}}}"
      },
      "params": {
      },
      "classes": [
        {
          "uid": "class_001",
          "name": "ask.help",
          "expressions": [
            "Can you help me?",
            "How does this work?",
            "I don't understand",
            "I need help",
            "I'm confused",
            "I'm having trouble",
            "I'm in need of help",
            "I'm lost",
            "What can I say?",
            "You lost me",
            "a little help, please?",
            "what can you do?",
            "what kinds of things can you do?",
            "help"
          ]
        },
        {
          "uid": "class_002",
          "name": "ask.time",
          "expressions": [
            "the time?",
            "time right now?",
            "time",
            "what time is it right now?",
            "what time is it?",
            "what's the clock say?",
            "what's the hour?",
            "what's the time?"
          ]
        },
        {
          "uid": "class_003",
          "name": "say.hello",
          "expressions": [
            "good afternoon",
            "good evening",
            "good morning",
            "hello there",
            "hey there",
            "hi hi",
            "hi there",
            "hi there",
            "how's it going?",
            "what's up?",
            "allo",
            "hallo",
            "hello",
            "hello",
            "hello",
            "hey",
            "heya",
            "heya",
            "heya",
            "heya",
            "hi",
            "hi",
            "hi",
            "hiya",
            "hiya",
            "hola",
            "hola",
            "howdy",
            "howdy",
            "howdy",
            "sup",
            "yo"
          ]
        },
        {
          "uid": "class_004",
          "name": "say.bye",
          "expressions": [
            "adios",
            "bye",
            "bye bye",
            "bye for now",
            "exit",
            "good bye",
            "good night",
            "goodbye",
            "goodnight",
            "later",
            "quit",
            "see ya",
            "see you later"
          ]
        },
        {
          "uid": "class_005",
          "name": "worklist.search",
          "expressions": [
            "show {{worker:Milo}}'s {{status:open}} {{context:tickets}} from {{org:Dobbus}} {{date:since last week}}",
            "show {{worker:Janey}}'s {{status:open}} {{context:tickets}} from {{org:Twinton University}}",
            "show {{worker:Ned}}'s {{status:waiting}} {{context:tickets}}",
            "open {{worker:my}} {{context:notifications}}",
            "display {{worker:my}} {{context:notifications}} for {{date:today}}",
            "what are {{worker:my}} {{context:notifications}}?",
            "list {{worker:my}} {{context:notifications}}",
            "show me {{worker:my}} {{context:notifications}} {{date:since last week}}",
            "show {{worker:my}} {{context:notifications}}",
            "show {{context:notifications}}",
            "show {{context:tickets}} from {{org:Ghoux Games}} {{date:since last month}}",
            "show {{context:messages}} from {{contact:Giada at Fiaflux}} {{date:in the past 30 days}}",
            "open {{context:messages}} from {{org:Ines Lacroix}} {{date:in the past 30 days}}",
            "open {{worker:my}} {{status:unread}} {{context:tasks}}",
            "display {{worker:my}} {{context:tasks}}",
            "what are {{worker:my}} {{context:tasks}} for {{org:Zhang}}?",
            "what are {{worker:my}} {{context:tasks}}?",
            "show {{worker:Kina}}'s {{context:tickets}} {{date:from March 2016}}",
            "show {{worker:Karl}}'s {{context:messages}} {{date:since last Monday}}",
            "show {{worker:Mara}}'s {{status:unread}} {{context:notifications}}",
            "show {{org:Nechist}}'s {{context:tickets}} from {{date:this week}}",
            "list {{worker:my}} {{context:tasks}}",
            "show {{worker:my}} {{context:tasks}}",
            "show {{worker:my}} {{status:incomplete}} {{context:tasks}}",
            "show {{context:tasks}}",
            "show {{date:last month}}'s {{context:tickets}}",
            "show {{date:last week}}'s {{context:tasks}}"
          ]
        }
      ]
    }
  ]
}
{% endraw %}
</code>
</pre>

You should see the following:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/imported.png" class="screenshot">
</div>

# Start a conversation with the bot

Click on the logo in the top left to return to your default page.

You should now see a floating bot icon in the lower right.

Click on it and select **Cerb >> Start chat**:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/interaction.png" class="screenshot">
</div>

This starts a conversation with Chat Bot to demonstrate interactions:

Try typing the following messages:

- `hi`
- `What time is it?`
- `find my open tickets`
- `I need help`

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/convo.png" class="screenshot">
</div>

You'll notice that the bot is helpful even when you don't mention _"help"_:

- `I'm lost and have no idea where to even begin`
- `What do I say?`
- `What can you do?`
- `please tell me what to say`

Similarly, you can get the current time with:

- `time`
- `the time?`
- `right now`

If you say `hi` or `time` multiple times you'll get back a few different variations.

# Learn how the behavior works

Navigate to **Search >> Bots** and open the card for **Cerb**.

On the card, click the **Behaviors** button.

Find the **Respond to worker chat** behavior and open its card.

You'll see the decision tree at the bottom of the popup:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree.png" class="screenshot">
</div>

## Using subroutines

At the top of level of the behavior there are three nodes with bold black labels that end with `()`:

- **say()**
- **worklistSearch()**
- **worklistSearchConfirmation()**

These are reusable sub-behaviors called [subroutines](/docs/bots/#subroutines).  Subroutines have access to the same dictionary of placeholders as the overall behavior.  You can _call_ a subroutine any number of times throughout a behavior by using actions, but a subroutine will never run on its own.

Let's take a closer look at the **say()** subroutine.  It has one action:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree-subroutine-say.png" class="screenshot">
</div>

It's pretty simple.  Every time the subroutine is called, it reads the value of the `say` placeholder and sends it to the worker as a chat message using the **Respond with message** action.  We can send a message back to the worker from anywhere in the behavior by writing some text to the `say` placeholder and then invoking `say()`.

You may be wondering why we bother to _wrap_ this simple action in a subroutine instead of using it directly every time we want to respond to the worker.  That will become very clear by the end of this guide.  In short, the `say()` subroutine allows the bot to also perform other actions every time it sends a message.  What you see here is the simplest example to start with.

## Determine intent from the chat message

Now we know how to some some text back to a worker using the `say()` subroutine.  It would be a good idea for our bot to figure out what the worker needs to accomplish.

As a listener on the **[UI] New chat message from worker** [event](/docs/bots/#events), the bot's behavior receives a [dictionary](/docs/bots/#dictionaries) with placeholders for the current worker and the message that they sent.

The first thing that the behavior does is run an [action](/docs/bots/#actions) called **Detect intent from chat message with a classifier**:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree-action-classifier.png" class="screenshot">
</div>

This sends the `{% raw %}message{% endraw %}` placeholder (the worker's chat message) to the **Detect Intent** [classifier](/docs/classifiers/) and receives back a prediction that it saves as `{% raw %}_prediction{% endraw %}`.  This helps us figure out what the worker is trying to accomplish.  We call that their _intent_.

The `_prediction` placeholder is a JSON object with this structure:

<pre>
<code class="language-json">
{% raw %}
{
	"text": "I need some help"
	"classifier": {
		"id": 1,
		"name": "Detect Intent"
	},
	"classification": {
		"id": 1,
		"name": "ask.help"
	},
	"confidence": 0.95,
	"params": [
		// Detected entities: dates, times, workers, contacts, etc.
	]
}
{% endraw %}
</code>
</pre>

## React to the intent

Since we're just interested in the predicted intent right now, we can use the `{% raw %}_prediction.classification.name{% endraw %}` placeholder in a decision.

That's exactly what the behavior does next. It makes a decision called **Intent:** with a few possible outcomes:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree-decision-intent.png" class="screenshot">
</div>

The **(new conversation)** outcome is special -- it matches when the chat message is empty.  This happens when you first open the chat window, and it allows the bot to speak first (letting you know how it can help).

The other outcomes just check the `{% raw %}_prediction.classification.name{% endraw %}` placeholder and compare it to a specific classification name:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree-outcome-intent.png" class="screenshot">
</div>

The first outcome that matches will continue running and the others will be ignored.

Most of the outcomes respond with some text as an action. For example, here's **say.hello**:

<div class="cerb-screenshot">
<img src="/assets/images/packages/chat-bot/cerb-behavior-tree-action-say-hello.png" class="screenshot">
</div>

This may look a little complicated if you haven't used placeholder scripting in Cerb's bots or [snippets](/docs/tickets/#snippets) before, so let's go through what it's doing.

Our goal is to break up the monotony of common responses by adding a few variations.  In this case, the bot may respond with _"hey"_, _"hi"_, _"howdy"_, etc.

To accomplish that, we're creating an _array_ of possible responses in the `r` _variable_ (_'r'_ as in _responses_).  That basic syntax is:

<pre>
<code class="language-twig">
{% raw %}
{% set r = ['hi','hey','hello'] %}
{% endraw %}
</code>
</pre>

For readability, we're putting each array member on a separate line.  For the above example, that looks like:

<pre>
<code class="language-twig">
{% raw %}
{% set r = [
	'hi',
	'hey',
	'hello'
] %}
{% endraw %}
</code>
</pre>

For each of those responses we want to address the worker by their first name.  We already have a dictionary of worker placeholders, so we can use `worker_first_name`.

In scripting, a sequence of text is called a _string_.  The process of joining multiple strings together into a single string is called _concatenation_.  The `~` (tilde) operator is used to concatenate strings in scripts.

Now we have an array named `r` that contains six variations of _"hello"_; each with the worker's first name appended to it.

We want to select one of those responses at random and send it to the worker.  We do that with the `random()` function, which accepts an array as an argument.  We give it our `r` responses array.

The output of that script is then saved to a new placeholder named `say`.

Finally, we call the `say()` subroutine that we talked about earlier, which takes the `say` placeholder we just set and sends its contents back to the worker as a chat message.

# Next steps

### Adding speech

A little earlier we hinted at the future advantages of using the `say()` subroutine every time the bot sends a message back to the worker.  One of those advantages is the ability to also speak the messages that we're sending.  Since all of our messages are routed through a single subroutine it's surprisingly simple to do.

The [Give Cerb bots the power of speech with Amazon Polly](/guides/integrations/aws/polly-speech/) guide uses the conversational bot we just created to demonstrate how to add speech to your bot.  It's a great next step.

# References

[^chatbot]: Wikipedia: Chatbot - <https://en.wikipedia.org/wiki/Chatbot>
[^ipa]: Wikipedia: Intelligent Personal Assistant - <https://en.wikipedia.org/wiki/Intelligent_personal_assistant>