<template>
  <div>
    2222
  </div>
</template>

<script>
    import * as _ from 'lodash';
    import ConditionExit from './condition_exit.vue';

    import {validators} from '_validators';
    
    const {required, jsExpressionNonEmptyString, validateIf} = validators;

    export default {
        components : {
            ConditionExit
        },

        props :   {
            template : {
                type : Object,
                default () {
                    return {}
                }
            },
            schema : {
                type : Object,
                default () {
                    return {}
                }
            },
            stepId : '',
            steps  : {
                type : Array,
                default () {
                    return []
                }
            },
            readonly : {
                type : Boolean,
                default : false
            }
        },

        data () {
            return {
                conditionExits  : _.get(this.schema, 'conditionExits') || [],
                singleExitRules : _.get(this.schema, 'singleExitRules') || {
                        rules: [
                            {
                                secondValue  : '``',
                                firstValue   : '``',
                                valueType    : 'string',
                                ruleType     : 'contains',
                                ruleCodeMode : false,
                                codeValue    : '',
                                dataOut      : '``'
                            }
                        ]
                    },
                newCondition () {
                    return {
                        label          : 'New Exit',
                        trueValue      : 'any',
                        rules          : [
                            {
                                secondValue  : '``',
                                firstValue   : '``',
                                valueType    : 'string',
                                ruleType     : 'contains',
                                ruleCodeMode : false,
                                codeValue    : '',
                                dataOut      : '``'
                            }
                        ] 
                    }
                }
            };
        },

        computed : {
            isSingleExit () {
                return this.template.isSingleExit;
            },

            conditionRuleHasDataOut () {
                return this.template.conditionRuleHasDataOut;
            }
        },

        watch : {
            conditionExits : {
                handler (newValue) {
                    this.schema.conditionExits = newValue;
                },
                deep : true
            },

            singleExitRules : {
                handler (newValue) {
                    console.log('singleExitRules', newValue);
                    this.schema.singleExitRules = newValue;
                },
                deep : true
            },

            schema : {
                handler (newValue) {
                    console.log('schema', newValue)
                },
                deep : true
            },

            template : {
                handler (newValue) {
                    if (!newValue.isSingleExit && _.isEmpty(this.conditionExits)) {
                        this.$nextTick(() => {
                            this.$refs['conditionExits'].addItem()
                        });
                    }
                },
                deep: true
            }
        },

        methods : {
            calculateExitLabel (item) {
                // if(_.isEmpty(item.label)) return 'No Name';

                // const label = item.label;
                // return `${label.length > 8 ? label.slice(0,8)+'...' : label}`;
            },
            
            updateExits (params) {
                // if (!_.isEmpty(this.schema.exits)) {
                //     if (_.isEmpty(params.oldItems) && _.isEmpty(params.newItems)) {
                //         // Items reordered
                //         const newDynamicExits = _.map(params.allItems, item => {
                //             const exit = _.find(this.schema.exits, {id : item.vforkey});
                //             return {
                //                 id : item.vforkey,
                //                 label : this.calculateExitLabel(item),
                //                 stepId : exit ? exit.stepId : ''
                //             };
                //         });
                //         try {
                //             _.forEach(newDynamicExits, (item, index) => {
                //                 const exitIndex = index;
                //                 this.schema.exits[exitIndex].id = item.id;
                //                 this.schema.exits[exitIndex].label = item.label;
                //                 this.schema.exits[exitIndex].stepId = item.stepId;
                //             }); 
                //         } catch(e) {
                //             console.log(e);
                //         }
                //     } else if (_.isEmpty(params.oldItems) && !_.isEmpty(params.newItems)) {
                //         // Item added
                //         const newItem = params.newItems[0];
                //         const lastDynamicExitIndex = _.findLastIndex(this.schema.exits, {dynamic : true});
                //         const index = lastDynamicExitIndex === -1 ? 0 : lastDynamicExitIndex + 1;
                //         this.schema.exits.splice(index, 0, {
                //             label    : this.calculateExitLabel(newItem),
                //             id       : newItem.vforkey,
                //             stepId   : '',
                //             dynamic  : true
                //         });
                //     } else if (!_.isEmpty(params.oldItems) && _.isEmpty(params.newItems)) {
                //         // Item removed
                //         const removedItem = params.oldItems[0];
                //         this.schema.exits.splice(_.findIndex(this.schema.exits, {id : removedItem.vforkey}), 1);
                //     } else if (!_.isEmpty(params.oldItems) && !_.isEmpty(params.newItems)) {
                //         // Item updated
                //         const oldItemValue = params.oldItems[0];
                //         const newItemValue = params.newItems[0];
                //         const changedItemIndex = _.findIndex(this.schema.exits, {id : oldItemValue.vforkey});
                //         this.schema.exits[changedItemIndex].id = newItemValue.vforkey;
                //         this.schema.exits[changedItemIndex].label = this.calculateExitLabel(newItemValue);
                //     }
                // }
            }
        },

        mounted () {
            // if (_.isEmpty(this.conditionExits) && !this.isSingleExit) {
            //     this.$refs['conditionExits'].addItem();
            // }
        },

        validations () {
            return {
                schema : validator(this.template)
            };
        }

    };

    export const data = (template) => ({
        isSingleExit            : template.isSingleExit,
        conditionRuleHasDataOut : template.conditionRuleHasDataOut,
        conditionExits          : template.conditionExits,
        singleExitRules         : template.singleExitRules
    });

    export const validator = (template) => {
        return {};
    };

    export const meta = {
        name    : 'condition-builder-component',
        type    : 'onereach-studio-form-editor',
        version : '0.5.0'
    };
</script>