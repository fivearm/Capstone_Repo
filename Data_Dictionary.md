|feature|type|description|
|-------|-----------|------|
|geo_level_1_id, geo_level_2_id, geo_level_3_id |int| geographic region in which building exists, from largest (level 1) to most specific sub-region (level 3). Possible values level 1 0-30, level 2 0-1427, level 3 0-12567.|
|count_floors_pre_eq |int| number of floors in the building before the earthquake.
|age |int| age of the building in years.|
|area_percentage |int| normalized area of the building footprint.|
|height_percentage |int| normalized height of the building footprint.|
|land_surface_condition |categorical| surface condition of the land where the building was built. Possible values: n, o, t.|
|foundation_type |categorical| type of foundation used while building. Possible values: h, i, r, u, w.|
|roof_type |categorical| type of roof used while building. Possible values: n, q, x.|
|ground_floor_type |categorical| type of the ground floor. Possible values: f, m, v, x, z.|
|other_floor_type |categorical| type of constructions used in higher than the ground floors |except of roof|. Possible values: j, q, s, x.|
|position |categorical| position of the building. Possible values: j, o, s, t.|
|plan_configuration |categorical| building plan configuration. Possible values: a, c, d, f, m, n, o, q, s, u.|
|has_superstructure_adobe_mud |binary| flag variable that indicates if the superstructure was made of Adobe/Mud.|
|has_superstructure_mud_mortar_stone |binary| flag variable that indicates if the superstructure was made of Mud Mortar - Stone.|
|has_superstructure_stone_flag |binary| flag variable that indicates if the superstructure was made of Stone.|
|has_superstructure_cement_mortar_stone |binary| flag variable that indicates if the superstructure was made of Cement Mortar - Stone.|
|has_superstructure_mud_mortar_brick |binary| flag variable that indicates if the superstructure was made of Mud Mortar - Brick.|
|has_superstructure_cement_mortar_brick |binary| flag variable that indicates if the superstructure was made of Cement Mortar - Brick.|
|has_superstructure_timber |binary| flag variable that indicates if the superstructure was made of Timber.|
|has_superstructure_bamboo |binary| flag variable that indicates if the superstructure was made of Bamboo.|
|has_superstructure_rc_non_engineered |binary| flag variable that indicates if the superstructure was made of non-engineered reinforced concrete.|
|has_superstructure_rc_engineered |binary| flag variable that indicates if the superstructure was made of engineered reinforced concrete.|
|has_superstructure_other |binary| flag variable that indicates if the superstructure was made of any other material.|
|legal_ownership_status |categorical| legal ownership status of the land where building was built. Possible values: a, r, v, w.|
|count_families |int| number of families that live in the building.|
|has_secondary_use |binary| flag variable that indicates if the building was used for any secondary purpose.|
|has_secondary_use_agriculture |binary| flag variable that indicates if the building was used for agricultural purposes.|
|has_secondary_use_hotel |binary| flag variable that indicates if the building was used as a hotel.|
|has_secondary_use_rental |binary| flag variable that indicates if the building was used for rental purposes.|
|has_secondary_use_institution |binary| flag variable that indicates if the building was used as a location of any institution.|
|has_secondary_use_school |binary| flag variable that indicates if the building was used as a school.|
|has_secondary_use_industry |binary| flag variable that indicates if the building was used for industrial purposes.|
|has_secondary_use_health_post |binary| flag variable that indicates if the building was used as a health post.|
|has_secondary_use_gov_office |binary| flag variable that indicates if the building was used fas a government office.|
|has_secondary_use_use_police |binary| flag variable that indicates if the building was used as a police station.|
|has_secondary_use_other |binary| flag variable that indicates if the building was secondarily used for other purposes.|
