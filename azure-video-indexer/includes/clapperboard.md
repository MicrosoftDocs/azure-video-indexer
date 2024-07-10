---
title: Clapper board detection
ms.service: azure-video-indexer
ms.topic: include
ms.date: 07/09/2024
ms.author: inhenkel
---

## Post-production: clapper board detection

[Clapper board](https://en.wikipedia.org/wiki/Clapperboard) detection detects clapper boards used during filming that also provides the information detected on the clapper board as metadata, for example, *production*, *roll*, *scene*, *take*, etc. Clapper board is part of the post-production insights that you can select in the web portal [advanced settings](../indexing-configuration-guide.md?#advanced-settings) when you upload and index the file.

## Clapper board use cases

Clapper board detection is most commonly used for post-production editing of visual media.

[!INCLUDE [Insights introductory paragraph](insights-intro-paragraph.md)]

### [Example responses](#tab/clapperboardresponse)

This response shows all of the data that come from detecting clapper boards. If you would like to learn more about how clapper boards are used in media production, check out the [video from Studio Binder](https://www.youtube.com/watch?v=Heg6kDxXZ8k) that was indexed for this example.

#### Clapper board detection

```json
"clapperboards": [
                    {
                        "id": 1,
                        "thumbnailId": "5a3714b9-a52b-4b3e-980a-ddf95c62033d",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "RJ NICHOLS"
                            },
                            {
                                "title": "date",
                                "content": "7.30.79 FYT"
                            },
                            {
                                "title": "director",
                                "content": "RJ NICHOLS"
                            },
                            {
                                "title": "production",
                                "content": "THE FARMERS DAUGHTERS"
                            },
                            {
                                "title": "roll",
                                "content": "1"
                            },
                            {
                                "title": "scene",
                                "content": "4"
                            },
                            {
                                "title": "sound",
                                "content": "T"
                            },
                            {
                                "title": "take",
                                "content": "4"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:07.9439122",
                                "adjustedEnd": "0:00:09.6183643",
                                "start": "0:00:07.9439122",
                                "end": "0:00:09.6183643"
                            }
                        ]
                    },
                    {
                        "id": 2,
                        "thumbnailId": "6b79c7dd-6d10-43dd-a2ac-c452437ebac7",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "ELIOT ROCKETT"
                            },
                            {
                                "title": "date",
                                "content": "BO24"
                            },
                            {
                                "title": "director",
                                "content": "SARAH POLLEY"
                            },
                            {
                                "title": "roll",
                                "content": "14151"
                            },
                            {
                                "title": "scene",
                                "content": "31C 1"
                            },
                            {
                                "title": "take",
                                "content": "800"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:10.280357",
                                "adjustedEnd": "0:00:10.5529422",
                                "start": "0:00:10.280357",
                                "end": "0:00:10.5529422"
                            }
                        ]
                    },
                    {
                        "id": 3,
                        "thumbnailId": "9cfcd99c-c885-4e02-96fa-47e8515076cb",
                        "isHeadSlate": false,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "DARIUSZ WOLSKI,"
                            },
                            {
                                "title": "director",
                                "content": "RIDLEY SCOTT"
                            },
                            {
                                "title": "scene",
                                "content": "3013"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:16.3551134",
                                "adjustedEnd": "0:00:18.26321",
                                "start": "0:00:16.3551134",
                                "end": "0:00:18.26321"
                            }
                        ]
                    },
                    {
                        "id": 4,
                        "thumbnailId": "eb89540b-9bfd-4128-98a2-eef35ebcf063",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "ELIOT ROCKETT"
                            },
                            {
                                "title": "date",
                                "content": "12/05/2021 5600 K"
                            },
                            {
                                "title": "director",
                                "content": "TI WEST"
                            },
                            {
                                "title": "roll",
                                "content": "309.02. 17. 19"
                            },
                            {
                                "title": "scene",
                                "content": "95E"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:00:50.9344963",
                                "adjustedEnd": "0:00:55.879971",
                                "start": "0:00:50.9344963",
                                "end": "0:00:55.879971"
                            }
                        ]
                    },
                    {
                        "id": 5,
                        "thumbnailId": "ea12f855-d23e-434b-9d10-f57bd65fb292",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "director",
                                "content": "OTTO WAGMAN"
                            },
                            {
                                "title": "production",
                                "content": "A GERMAN AFFAIR"
                            },
                            {
                                "title": "scene",
                                "content": "20"
                            },
                            {
                                "title": "take",
                                "content": "2"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:01:05.4204539",
                                "adjustedEnd": "0:01:12.0014401",
                                "start": "0:01:05.4204539",
                                "end": "0:01:12.0014401"
                            }
                        ]
                    },
                    {
                        "id": 6,
                        "thumbnailId": "838a70ab-ccd7-4244-8cc4-e7d8a1c98d22",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "SQUARE"
                            },
                            {
                                "title": "date",
                                "content": "16 JAN '17"
                            },
                            {
                                "title": "director",
                                "content": "PAUL THOMAS ANDERSON"
                            },
                            {
                                "title": "scene",
                                "content": "3 FITEROY"
                            },
                            {
                                "title": "slate",
                                "content": "8"
                            },
                            {
                                "title": "take",
                                "content": "-"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:01:40.9344146",
                                "adjustedEnd": "0:01:43.3098002",
                                "start": "0:01:40.9344146",
                                "end": "0:01:43.3098002"
                            }
                        ]
                    },
                    {
                        "id": 7,
                        "thumbnailId": "f9ea5590-5c36-4fcb-afaf-b8a73e20c45c",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Tom Stern. asc. afc"
                            },
                            {
                                "title": "director",
                                "content": "Clint Eastwood"
                            },
                            {
                                "title": "take",
                                "content": "15.32.05. 17"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:01:52.3829941",
                                "adjustedEnd": "0:01:52.6555793",
                                "start": "0:01:52.3829941",
                                "end": "0:01:52.6555793"
                            }
                        ]
                    },
                    {
                        "id": 8,
                        "thumbnailId": "8d9025c4-fe66-40b4-be51-b1736d7023f8",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Ed Lachman, ASC"
                            },
                            {
                                "title": "director",
                                "content": "Todd Haynes"
                            },
                            {
                                "title": "roll",
                                "content": "B63"
                            },
                            {
                                "title": "scene",
                                "content": "B63"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:01:59.8596174",
                                "adjustedEnd": "0:02:03.4032253",
                                "start": "0:01:59.8596174",
                                "end": "0:02:03.4032253"
                            }
                        ]
                    },
                    {
                        "id": 9,
                        "thumbnailId": "d190d0fc-0feb-4881-838d-2a29e92962a3",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Eric Steelberg"
                            },
                            {
                                "title": "director",
                                "content": "Marc Webb 05/20/08"
                            },
                            {
                                "title": "scene",
                                "content": "4/B"
                            },
                            {
                                "title": "take",
                                "content": "77"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:02:05.7007294",
                                "adjustedEnd": "0:02:05.9733146",
                                "start": "0:02:05.7007294",
                                "end": "0:02:05.9733146"
                            }
                        ]
                    },
                    {
                        "id": 10,
                        "thumbnailId": "f71a1482-7eeb-432d-950f-39eb901ce86d",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Eric Steelberg"
                            },
                            {
                                "title": "director",
                                "content": "Marc Webb 05/20/08"
                            },
                            {
                                "title": "scene",
                                "content": "4/B"
                            },
                            {
                                "title": "take",
                                "content": "77"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:02:06.6353073",
                                "adjustedEnd": "0:02:07.141537",
                                "start": "0:02:06.6353073",
                                "end": "0:02:07.141537"
                            }
                        ]
                    },
                    {
                        "id": 11,
                        "thumbnailId": "07a511e8-5746-483d-95a3-54d89fc08780",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Brendan Galvin ISC"
                            },
                            {
                                "title": "date",
                                "content": "9/1/21"
                            },
                            {
                                "title": "director",
                                "content": "Brendan Galvin ISC"
                            },
                            {
                                "title": "take",
                                "content": "9/1/21"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:02:08.0371741",
                                "adjustedEnd": "0:02:14.6181603",
                                "start": "0:02:08.0371741",
                                "end": "0:02:14.6181603"
                            }
                        ]
                    },
                    {
                        "id": 12,
                        "thumbnailId": "de1058c3-ab0f-4c45-bfef-b3c8bb9b7654",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "J CRONENWETH"
                            },
                            {
                                "title": "director",
                                "content": "R. SCOTT"
                            },
                            {
                                "title": "scene",
                                "content": "123"
                            },
                            {
                                "title": "take",
                                "content": "409651"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:02:35.1399336",
                                "adjustedEnd": "0:02:35.4125189",
                                "start": "0:02:35.1399336",
                                "end": "0:02:35.4125189"
                            }
                        ]
                    },
                    {
                        "id": 13,
                        "thumbnailId": "c6822574-fa28-4b9a-aca2-8c6514858e04",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Ed Lachman, ASC"
                            },
                            {
                                "title": "director",
                                "content": "Todd Haynes"
                            },
                            {
                                "title": "roll",
                                "content": "44"
                            },
                            {
                                "title": "scene",
                                "content": "44"
                            },
                            {
                                "title": "take",
                                "content": "44"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:02:40.5137566",
                                "adjustedEnd": "0:02:49.8984765",
                                "start": "0:02:40.5137566",
                                "end": "0:02:49.8984765"
                            }
                        ]
                    },
                    {
                        "id": 14,
                        "thumbnailId": "0b80ceff-e468-4c7d-b3dc-4e3adc18d2f3",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Bobby Bukowski"
                            },
                            {
                                "title": "director",
                                "content": "Chinonye Chukwu"
                            },
                            {
                                "title": "roll",
                                "content": "8"
                            },
                            {
                                "title": "scene",
                                "content": "[ the social network ]"
                            },
                            {
                                "title": "take",
                                "content": "13"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:03:29.1118082",
                                "adjustedEnd": "0:03:31.7208382",
                                "start": "0:03:29.1118082",
                                "end": "0:03:31.7208382"
                            }
                        ]
                    },
                    {
                        "id": 15,
                        "thumbnailId": "76b4b21e-6534-438d-9b87-2f46a14b9065",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "CRONENWETH. ASC"
                            },
                            {
                                "title": "director",
                                "content": "FINCHER"
                            },
                            {
                                "title": "scene",
                                "content": "[ the social network]"
                            },
                            {
                                "title": "take",
                                "content": "17"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:03:32.3828309",
                                "adjustedEnd": "0:03:34.057283",
                                "start": "0:03:32.3828309",
                                "end": "0:03:34.057283"
                            }
                        ]
                    },
                    {
                        "id": 16,
                        "thumbnailId": "632c45a1-3a06-4fbc-bd18-cec77d1532d5",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "INFORMATION (if appropriate)"
                            },
                            {
                                "title": "date",
                                "content": "8/3/01"
                            },
                            {
                                "title": "episode",
                                "content": "-"
                            },
                            {
                                "title": "production",
                                "content": "HIGH TIDE"
                            },
                            {
                                "title": "roll",
                                "content": "-"
                            },
                            {
                                "title": "scene",
                                "content": "SLATE/IDENT"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:03:53.6444784",
                                "adjustedEnd": "0:03:56.0198639",
                                "start": "0:03:53.6444784",
                                "end": "0:03:56.0198639"
                            }
                        ]
                    },
                    {
                        "id": 17,
                        "thumbnailId": "460f2b19-ba22-4599-a921-7e3a72ee8b9e",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "BEN LOEB"
                            },
                            {
                                "title": "date",
                                "content": "OA"
                            },
                            {
                                "title": "director",
                                "content": "PANOS COSMATOS"
                            },
                            {
                                "title": "scene",
                                "content": "ilter"
                            },
                            {
                                "title": "take",
                                "content": "20/2 1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:05:58.4106299",
                                "adjustedEnd": "0:06:01.7205933",
                                "start": "0:05:58.4106299",
                                "end": "0:06:01.7205933"
                            }
                        ]
                    },
                    {
                        "id": 18,
                        "thumbnailId": "718bf850-34f4-4da3-ae04-db1cf978b057",
                        "isHeadSlate": false,
                        "fields": [
                            {
                                "title": "date",
                                "content": "A69"
                            },
                            {
                                "title": "director",
                                "content": "OF PHOTOGRAPHY"
                            },
                            {
                                "title": "roll",
                                "content": "11/19 12"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:04.4853863",
                                "adjustedEnd": "0:06:04.5243271",
                                "start": "0:06:04.4853863",
                                "end": "0:06:04.5243271"
                            }
                        ]
                    },
                    {
                        "id": 19,
                        "thumbnailId": "045c72e6-7a6f-4aab-92cc-4e8b48e45e63",
                        "isHeadSlate": false,
                        "fields": [
                            {
                                "title": "date",
                                "content": "A69"
                            },
                            {
                                "title": "director",
                                "content": "OF PHOTOGRAPHY"
                            },
                            {
                                "title": "take",
                                "content": "124"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:04.9526753",
                                "adjustedEnd": "0:06:04.991616",
                                "start": "0:06:04.9526753",
                                "end": "0:06:04.991616"
                            }
                        ]
                    },
                    {
                        "id": 20,
                        "thumbnailId": "f1d1b2ff-8ae1-4fe2-a038-b1312610e33a",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "DARIUS KHONDJI"
                            },
                            {
                                "title": "date",
                                "content": "DARIUS KHONDJI"
                            },
                            {
                                "title": "director",
                                "content": "JAMES GRAY"
                            },
                            {
                                "title": "roll",
                                "content": "10.44.52.08"
                            },
                            {
                                "title": "scene",
                                "content": "47C 2 /u"
                            },
                            {
                                "title": "take",
                                "content": "10.44.5 126"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:16.6348992",
                                "adjustedEnd": "0:06:18.7766403",
                                "start": "0:06:16.6348992",
                                "end": "0:06:18.7766403"
                            }
                        ]
                    },
                    {
                        "id": 21,
                        "thumbnailId": "7ed00ad4-7b8b-4167-a408-e4aa9335636b",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1S/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:26.9152563",
                                "adjustedEnd": "0:06:26.954197",
                                "start": "0:06:26.9152563",
                                "end": "0:06:26.954197"
                            }
                        ]
                    },
                    {
                        "id": 22,
                        "thumbnailId": "9c8cf59b-8781-412a-9683-6362c6d36166",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "11//5/17"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:28.0834787",
                                "adjustedEnd": "0:06:28.5897084",
                                "start": "0:06:28.0834787",
                                "end": "0:06:28.5897084"
                            }
                        ]
                    },
                    {
                        "id": 23,
                        "thumbnailId": "b5a95e35-1403-47de-a7fa-7823cc6e45ac",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1S/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "20 .-"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:29.251701",
                                "adjustedEnd": "0:06:29.7579307",
                                "start": "0:06:29.251701",
                                "end": "0:06:29.7579307"
                            }
                        ]
                    },
                    {
                        "id": 24,
                        "thumbnailId": "18f60187-996f-4c16-9034-238821de4a1b",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1/IS/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:30.6535679",
                                "adjustedEnd": "0:06:32.32802",
                                "start": "0:06:30.6535679",
                                "end": "0:06:32.32802"
                            }
                        ]
                    },
                    {
                        "id": 25,
                        "thumbnailId": "77b284e6-a1b6-4cad-8388-19b79a79406c",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1S/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:32.7563682",
                                "adjustedEnd": "0:06:33.0289534",
                                "start": "0:06:32.7563682",
                                "end": "0:06:33.0289534"
                            }
                        ]
                    },
                    {
                        "id": 26,
                        "thumbnailId": "eec78d65-61a1-4a3e-8968-5f25ea9586c1",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1/S/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "20000"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:34.3918796",
                                "adjustedEnd": "0:06:34.4308203",
                                "start": "0:06:34.3918796",
                                "end": "0:06:34.4308203"
                            }
                        ]
                    },
                    {
                        "id": 27,
                        "thumbnailId": "b3f0f9c0-3f01-445c-a0d1-3fdc0dedd209",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "1/IS/IT"
                            },
                            {
                                "title": "roll",
                                "content": "24"
                            },
                            {
                                "title": "take",
                                "content": "20 .-"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:35.3264575",
                                "adjustedEnd": "0:06:36.5336206",
                                "start": "0:06:35.3264575",
                                "end": "0:06:36.5336206"
                            }
                        ]
                    },
                    {
                        "id": 28,
                        "thumbnailId": "5efcbd65-51a3-48b7-b5ab-c6f68378529b",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "8/10/20"
                            },
                            {
                                "title": "director",
                                "content": "TOM GORMICAN"
                            },
                            {
                                "title": "director of photography",
                                "content": "NIGEL BLUCK"
                            },
                            {
                                "title": "take",
                                "content": "3"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:41.1675694",
                                "adjustedEnd": "0:06:42.8420215",
                                "start": "0:06:41.1675694",
                                "end": "0:06:42.8420215"
                            }
                        ]
                    },
                    {
                        "id": 29,
                        "thumbnailId": "f3f1c454-c4a9-4f9f-97e6-88bba0bd0dae",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "22 11 2020"
                            },
                            {
                                "title": "director",
                                "content": "TOM GORMICAN"
                            },
                            {
                                "title": "director of photography",
                                "content": "NIGEL BLUCK"
                            },
                            {
                                "title": "slate",
                                "content": "100"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:43.9713032",
                                "adjustedEnd": "0:06:44.4775329",
                                "start": "0:06:43.9713032",
                                "end": "0:06:44.4775329"
                            }
                        ]
                    },
                    {
                        "id": 30,
                        "thumbnailId": "064feadf-71c1-4cef-93c5-f3edb2b6c879",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "READY PLAYER ONE (BTS)"
                            },
                            {
                                "title": "director",
                                "content": "STEVEN SPIELBERG"
                            },
                            {
                                "title": "slate",
                                "content": "15 19 0"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:06:45.1395256",
                                "adjustedEnd": "0:06:46.8139777",
                                "start": "0:06:45.1395256",
                                "end": "0:06:46.8139777"
                            }
                        ]
                    },
                    {
                        "id": 31,
                        "thumbnailId": "62c4f400-a404-41ed-a79a-d2ece0774555",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "DARREN ARONOFSKY"
                            },
                            {
                                "title": "date",
                                "content": "DARREN ARONOFSKY"
                            },
                            {
                                "title": "director",
                                "content": "NOAH"
                            },
                            {
                                "title": "roll",
                                "content": "1"
                            },
                            {
                                "title": "scene",
                                "content": "V154"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:07:01.7282836",
                                "adjustedEnd": "0:07:06.4401139",
                                "start": "0:07:01.7282836",
                                "end": "0:07:06.4401139"
                            }
                        ]
                    },
                    {
                        "id": 32,
                        "thumbnailId": "ad19a26d-c601-4073-b0de-f0e3d072390e",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "JOHN SEAL"
                            },
                            {
                                "title": "director",
                                "content": "GEORGE MILLER"
                            },
                            {
                                "title": "roll",
                                "content": "18"
                            },
                            {
                                "title": "scene",
                                "content": "XM 1b.34.08.88"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:07:08.7376179",
                                "adjustedEnd": "0:07:08.7765587",
                                "start": "0:07:08.7376179",
                                "end": "0:07:08.7765587"
                            }
                        ]
                    },
                    {
                        "id": 33,
                        "thumbnailId": "435e12dc-56c3-473e-8e30-1be97e23c68e",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "WAGNER"
                            },
                            {
                                "title": "date",
                                "content": "ECTOR"
                            },
                            {
                                "title": "director",
                                "content": "PICTURE"
                            },
                            {
                                "title": "production",
                                "content": "CO."
                            },
                            {
                                "title": "roll",
                                "content": "4"
                            },
                            {
                                "title": "scene",
                                "content": "KINOSCOPE PICTURES"
                            },
                            {
                                "title": "sound",
                                "content": "MORROW"
                            },
                            {
                                "title": "take",
                                "content": "63"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:07:28.8310431",
                                "adjustedEnd": "0:07:38.2157629",
                                "start": "0:07:28.8310431",
                                "end": "0:07:38.2157629"
                            }
                        ]
                    },
                    {
                        "id": 34,
                        "thumbnailId": "f9fc81a7-bc8c-478a-a418-0e4ad03705f3",
                        "isHeadSlate": false,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "DARIUSZ WOLSKI, A"
                            },
                            {
                                "title": "director",
                                "content": "DIDLEY SCOTT"
                            },
                            {
                                "title": "scene",
                                "content": "3013"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:08:19.5318949",
                                "adjustedEnd": "0:08:21.6736359",
                                "start": "0:08:19.5318949",
                                "end": "0:08:21.6736359"
                            }
                        ]
                    },
                    {
                        "id": 35,
                        "thumbnailId": "8ac1aece-adf9-4600-9e5e-f11112f39341",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "A"
                            },
                            {
                                "title": "date",
                                "content": "FRIENDS"
                            },
                            {
                                "title": "director",
                                "content": "HOSPITAL HALLUCINATIC"
                            },
                            {
                                "title": "scene",
                                "content": "OLD"
                            },
                            {
                                "title": "take",
                                "content": "3"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:08:28.4103851",
                                "adjustedEnd": "0:08:30.0848372",
                                "start": "0:08:28.4103851",
                                "end": "0:08:30.0848372"
                            }
                        ]
                    },
                    {
                        "id": 36,
                        "thumbnailId": "26ae8a5e-9ee9-4d86-9455-5919c8877fa4",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "R. PRiETO"
                            },
                            {
                                "title": "date",
                                "content": "1-Ozan"
                            },
                            {
                                "title": "director",
                                "content": "M.BLANCO"
                            },
                            {
                                "title": "roll",
                                "content": "150"
                            },
                            {
                                "title": "scene",
                                "content": "CHiCAS Y MALETAS"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:09:26.8215047",
                                "adjustedEnd": "0:09:29.1968902",
                                "start": "0:09:26.8215047",
                                "end": "0:09:29.1968902"
                            }
                        ]
                    },
                    {
                        "id": 37,
                        "thumbnailId": "5d963d02-6e49-47f4-83e1-6dc5a2f6153a",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "LENS"
                            },
                            {
                                "title": "director",
                                "content": "MICHAEL B. JORDAN"
                            },
                            {
                                "title": "notes",
                                "content": "45-135/4/KMI6"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:09:40.8401734",
                                "adjustedEnd": "0:09:41.1127586",
                                "start": "0:09:40.8401734",
                                "end": "0:09:41.1127586"
                            }
                        ]
                    },
                    {
                        "id": 38,
                        "thumbnailId": "d14bcdaa-ec71-498f-9741-f9bb8e45f457",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "JAN-14 . 2009"
                            },
                            {
                                "title": "director of photography",
                                "content": "Robert Richardsde"
                            },
                            {
                                "title": "roll",
                                "content": "71"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:10:04.4382657",
                                "adjustedEnd": "0:10:04.4772064",
                                "start": "0:10:04.4382657",
                                "end": "0:10:04.4772064"
                            }
                        ]
                    },
                    {
                        "id": 39,
                        "thumbnailId": "79691bf8-6b75-462a-b5b7-7de91f552ffa",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "director",
                                "content": "Quentin Tarantino"
                            },
                            {
                                "title": "roll",
                                "content": "2009"
                            },
                            {
                                "title": "scene",
                                "content": "A1038A66A 3"
                            },
                            {
                                "title": "take",
                                "content": "2009"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:10:12.382178",
                                "adjustedEnd": "0:10:12.6547632",
                                "start": "0:10:12.382178",
                                "end": "0:10:12.6547632"
                            }
                        ]
                    },
                    {
                        "id": 40,
                        "thumbnailId": "cfdc3cba-0c07-4f26-9438-a5a97fc95f3c",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "D.P. MICHAEL SERESIN"
                            },
                            {
                                "title": "director",
                                "content": "MATT REEVES"
                            },
                            {
                                "title": "roll",
                                "content": "14.35.27. 10"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:10:16.5877786",
                                "adjustedEnd": "0:10:17.0940083",
                                "start": "0:10:16.5877786",
                                "end": "0:10:17.0940083"
                            }
                        ]
                    },
                    {
                        "id": 41,
                        "thumbnailId": "347852cc-dd77-4790-baa6-98b8865aee79",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "4-26-13"
                            },
                            {
                                "title": "director",
                                "content": "MATT REEVES"
                            },
                            {
                                "title": "roll",
                                "content": "10 30 24 70"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:10:17.5223565",
                                "adjustedEnd": "0:10:19.897742",
                                "start": "0:10:17.5223565",
                                "end": "0:10:19.897742"
                            }
                        ]
                    },
                    {
                        "id": 42,
                        "thumbnailId": "fb6e8ad0-1f9d-4a56-a3b5-3bb184f74c7b",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "08.15.2016"
                            },
                            {
                                "title": "director of photography",
                                "content": "Roger Deakins"
                            },
                            {
                                "title": "scene",
                                "content": "5BIIB3"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:11:02.8493853",
                                "adjustedEnd": "0:11:02.8883261",
                                "start": "0:11:02.8493853",
                                "end": "0:11:02.8883261"
                            }
                        ]
                    },
                    {
                        "id": 43,
                        "thumbnailId": "e0eef972-ac5d-4ac2-9e40-01965cc75f9a",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Filmrools"
                            },
                            {
                                "title": "date",
                                "content": "24/03/12"
                            },
                            {
                                "title": "director",
                                "content": "FILTER"
                            },
                            {
                                "title": "production",
                                "content": "PETER HENDERSON"
                            },
                            {
                                "title": "roll",
                                "content": "-"
                            },
                            {
                                "title": "scene",
                                "content": "LY50L-"
                            },
                            {
                                "title": "take",
                                "content": "3"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:11:25.5128997",
                                "adjustedEnd": "0:11:28.1219297",
                                "start": "0:11:25.5128997",
                                "end": "0:11:28.1219297"
                            }
                        ]
                    },
                    {
                        "id": 44,
                        "thumbnailId": "af74ae3f-acf1-4176-8a23-78da829a9aee",
                        "isHeadSlate": false,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "A REC"
                            },
                            {
                                "title": "director",
                                "content": "ALEX GAFLAHD DOP RE IWEPY UE"
                            },
                            {
                                "title": "director of photography",
                                "content": "ANNIHILATION (BTS)"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:11:55.8866819",
                                "adjustedEnd": "0:11:55.9256227",
                                "start": "0:11:55.8866819",
                                "end": "0:11:55.9256227"
                            }
                        ]
                    },
                    {
                        "id": 45,
                        "thumbnailId": "3bf82938-b00c-45a6-a95d-a1957b112369",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "DARIUSZ WOLSKI, ASC"
                            },
                            {
                                "title": "director",
                                "content": "RIDLEY SCOTT"
                            },
                            {
                                "title": "take",
                                "content": "1"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:12:07.1016169",
                                "adjustedEnd": "0:12:07.8414911",
                                "start": "0:12:07.1016169",
                                "end": "0:12:07.8414911"
                            }
                        ]
                    },
                    {
                        "id": 46,
                        "thumbnailId": "d777e3d5-2f54-4bcd-8732-821d403b2f7b",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "..."
                            },
                            {
                                "title": "scene",
                                "content": "SHOT"
                            },
                            {
                                "title": "shot",
                                "content": "SIZE"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:12:21.5875745",
                                "adjustedEnd": "0:12:22.7947377",
                                "start": "0:12:21.5875745",
                                "end": "0:12:22.7947377"
                            }
                        ]
                    },
                    {
                        "id": 47,
                        "thumbnailId": "32599397-b938-4641-9da1-f067cd306a8c",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "..."
                            },
                            {
                                "title": "scene",
                                "content": "SHOT"
                            },
                            {
                                "title": "shot",
                                "content": "TYPE"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:12:23.2230859",
                                "adjustedEnd": "0:12:24.897538",
                                "start": "0:12:23.2230859",
                                "end": "0:12:24.897538"
                            }
                        ]
                    },
                    {
                        "id": 48,
                        "thumbnailId": "8f26d7e7-3c61-4ca7-ae21-22f64332cd05",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "camera",
                                "content": "Pirector"
                            },
                            {
                                "title": "date",
                                "content": "CSs"
                            },
                            {
                                "title": "director",
                                "content": "mera"
                            },
                            {
                                "title": "take",
                                "content": "8/24/21"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:12:35.8398877",
                                "adjustedEnd": "0:12:38.4489177",
                                "start": "0:12:35.8398877",
                                "end": "0:12:38.4489177"
                            }
                        ]
                    },
                    {
                        "id": 49,
                        "thumbnailId": "41ef61c7-04a1-47e0-aba6-73cee255dbd8",
                        "isHeadSlate": true,
                        "fields": [
                            {
                                "title": "date",
                                "content": "mn.Francors Richet"
                            },
                            {
                                "title": "director",
                                "content": "mera"
                            },
                            {
                                "title": "take",
                                "content": "8/24/21"
                            }
                        ],
                        "instances": [
                            {
                                "adjustedStart": "0:12:40.2791328",
                                "adjustedEnd": "0:12:40.3180736",
                                "start": "0:12:40.2791328",
                                "end": "0:12:40.3180736"
                            }
                        ]
                    }
                ],
```

|Name|Description|
|---|---|
|`id`|The clapper board ID.|
|`thumbnailId`|The ID of the thumbnail.|
|`isHeadSlate`|The value stands for head or tail (the board is upside-down) of the clapper board: `true` or `false`.|
|`fields`|The fields found in the clapper board; also each field's name and value.|
|`instances`|A list of time ranges where this element appeared.|

### [Components](#tab/clapperboardcomponents)

No components are defined.

### [Transparency notes](#tab/clappertransnote)

- The values might not be correctly identified by the detection algorithm.
- The titles of the fields appearing on the clapper board are optimized to identify the most popular fields appearing on top of clapper boards.  
- Handwritten text or digital digits might not be correctly identified by the fields detection algorithm.
- The algorithm is optimized to identify fields' categories that appear horizontally.  
- The clapper board might not be detected if the frame is blurred or that the text written on it can't be read by the human eye.  
- Empty fields’ values might lead to wrong fields categories.

### [Sample code](#tab/clappersamplecode)

[See all samples for VI](https://github.com/Azure-Samples/azure-video-indexer-samples)

---
