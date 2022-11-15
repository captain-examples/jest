# Getting Captain working with Jest

Starting from a [simple workflow that runs jest][workflow-before-captain], we want to

1. 🧪 Ensure jest produces json output

`jest --json --outputFile tmp/jest.json` will produce Captain-compatible json output in `tmp/jest.json`. We get useful
location information if you also include `--testLocationInResults`

```sh
npm test -- --json --testLocationInResults --outputFile tmp/jest.json
```

2. 🔐 Create an Access Token

Create an Access Token for your organization within [Captain][captain-access-token] ([more documentation here][create-access-token]).

Add the new token as an action secret to your repository. Conventionally, we call this secret `RWX_ACCESS_TOKEN`.

3. 💌 Install the Captain CLI and call it when running tests

See the [full documentation on test suite integration][test-suite-integration].

```yaml
- uses: rwx-research/setup-captain@v1
- name: Run tests
  run: |
    captain run \
      --suite-id captain-examples-jest \
      --test-results tmp/jest.json \
      --  \
      npm test -- --json --outputFile=tmp/jest.json --testLocationInResults
  env:
    RWX_ACCESS_TOKEN: ${{ secrets.RWX_ACCESS_TOKEN }}
```

4. 🎉 See your test results in Captain!

Take a look at the [final workflow!][workflow-with-captain]

[workflow-before-captain]: https://github.com/captain-examples/jest/blob/basic-workflow/.github/workflows/ci.yml
[captain-access-token]: https://account.rwx.com/deep_link/manage/access_tokens
[create-access-token]: https://www.rwx.com/docs/access-tokens
[workflow-with-captain]: https://github.com/captain-examples/jest/blob/main/.github/workflows/ci.yml
[test-suite-integration]: https://www.rwx.com/captain/docs/test-suite-integration
