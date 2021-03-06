FROM node:12.16.2-alpine  as build-stage

ARG react_app_api_entrypoint
ARG react_app_title
ARG react_app_default_producer_logo
ARG react_app_eos_rate_link
ARG react_app_use_rewards
ARG react_app_use_votes
ARG react_app_use_block_producer_agreement_contract
ARG react_app_eos_api_host
ARG react_app_eos_api_port
ARG react_app_eos_api_protocol
ARG react_app_eos_chain_id
ARG react_app_eos_default_exchange_rate
ARG react_app_eos_default_exchange_rate_api
ARG react_app_eos_use_bp_json_on_chain
ARG react_app_eos_bp_json_on_chain_contract
ARG react_app_eos_bp_json_on_chain_table
ARG react_app_eos_bp_json_on_chain_scope
ARG react_app_eos_endpoint

ENV WORK_DIR /usr/src/app
ENV PATH $WORK_DIR/node_modules/.bin:$PATH
ENV NODE_ENV production
ENV NODE_PATH ./src
ENV REACT_APP_API_ENTRYPOINT $react_app_api_entrypoint
ENV REACT_APP_TITLE $react_app_title
ENV REACT_APP_DEFAULT_PRODUCER_LOGO $react_app_default_producer_logo
ENV REACT_APP_EOS_RATE_LINK $react_app_eos_rate_link
ENV REACT_APP_USE_REWARDS $react_app_use_rewards
ENV REACT_APP_USE_VOTES $react_app_use_votes
ENV REACT_APP_USE_BLOCK_PRODUCER_AGREEMENT_CONTRACT $react_app_use_block_producer_agreement_contract
ENV REACT_APP_EOS_API_HOST $react_app_eos_api_host
ENV REACT_APP_EOS_API_PORT $react_app_eos_api_port
ENV REACT_APP_EOS_API_PROTOCOL $react_app_eos_api_protocol
ENV REACT_APP_EOS_CHAIN_ID $react_app_eos_chain_id
ENV REACT_APP_EOS_DEFAULT_EXCHANGE_RATE $react_app_eos_default_exchange_rate
ENV REACT_APP_EOS_DEFAULT_EXCHANGE_RATE_API $react_app_eos_default_exchange_rate_api
ENV REACT_APP_EOS_USE_BP_JSON_ON_CHAIN $react_app_eos_use_bp_json_on_chain
ENV REACT_APP_EOS_BP_JSON_ON_CHAIN_CONTRACT $react_app_eos_bp_json_on_chain_contract
ENV REACT_APP_EOS_BP_JSON_ON_CHAIN_TABLE $react_app_eos_bp_json_on_chain_table
ENV REACT_APP_EOS_BP_JSON_ON_CHAIN_SCOPE $react_app_eos_bp_json_on_chain_scope
ENV REACT_APP_EOS_ENDPOINT $react_app_eos_endpoint

RUN mkdir -p $WORK_DIR
WORKDIR $WORK_DIR

COPY package.json $WORK_DIR/package.json
COPY yarn.lock $WORK_DIR/yarn.lock

RUN yarn install --frozen-lockfile --production=true

COPY ./ $WORK_DIR

RUN yarn build

FROM nginx:1.17.10-alpine as run-stage

COPY --from=build-stage /usr/src/app/build /usr/share/nginx/html
COPY --from=build-stage /usr/src/app/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

