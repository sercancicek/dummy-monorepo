# Customer Dwh Queries

[![ref_badge_t3]][ref_confluence_support_tiers]

Run DWH queries and paste into gsheets.

## Running the project

### Running `customer_dwh_queries` locally

Launch the main functionality, by running in the project root:

```shell
$ poetry install --sync --without dev
$ poetry run python -m customer_dwh_queries
```

> Note: Environment variables can be injected into the containers using `.env` file in
> the root of the project. Use `.env.example` as a base for your `.env` file, adding any
> needed environment variable.

> Note 2: `NEXUS_USERNAME`, `NEXUS_PASSWORD` and `EXAMPLE_PASSWORD` must be defined in
> the environment for the above commands to run.

## Testing and documenting the code

> Note: this part requires running `poetry install --sync` to install the dev
> dependencies.

### Running `pytest` test cases

To run the unit tests defined in the `tests` folder, in the project root run:

```shell
$ poetry run guide test
```

[ref_badge_t1]:
  https://picnic-global-prod-python-platform-public.s3.eu-west-1.amazonaws.com/ESE/badges/support_tier/t1.svg
[ref_badge_t2]:
  https://picnic-global-prod-python-platform-public.s3.eu-west-1.amazonaws.com/ESE/badges/support_tier/t2.svg
[ref_badge_t3]:
  https://picnic-global-prod-python-platform-public.s3.eu-west-1.amazonaws.com/ESE/badges/support_tier/t3.svg
[ref_badge_t4]:
  https://picnic-global-prod-python-platform-public.s3.eu-west-1.amazonaws.com/ESE/badges/support_tier/t4.svg
[ref_confluence_support_tiers]:
  https://picnic.atlassian.net/wiki/spaces/PY/pages/3778936975/
