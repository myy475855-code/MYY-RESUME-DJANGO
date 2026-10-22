# Risks and Mitigations

  -----------------------------------------------------------------------
  Risk                    Impact                  Mitigation
  ----------------------- ----------------------- -----------------------
  AI invents              User harm and loss of   Ground suggestions in
  qualifications          trust                   user facts; require
                                                  review; preserve
                                                  original content

  Misleading ATS score    Users may make poor     Disclose score
                          decisions               methodology and
                                                  limitations

  PDF layout defects      Poor user experience    Automated PDF tests,
                                                  representative
                                                  fixtures, visual review

  Malicious document      Security compromise     Strict validation,
  uploads                                         private storage,
                                                  isolated processing,
                                                  size limits

  Cross-user data         Serious privacy         Ownership-scoped
  exposure                incident                querysets,
                                                  authorization tests,
                                                  least privilege

  AI provider outage      Features unavailable    Timeouts, graceful
                                                  errors, retry only
                                                  transient failures

  High AI costs           Unsustainable unit      Quotas, token limits,
                          economics               cost monitoring,
                                                  pricing experiments

  Scope creep             Delayed launch          Keep MVP boundaries and
                                                  phase later features

  Low retention           Weak startup traction   Interview users,
                                                  measure repeated value,
                                                  improve the job
                                                  workflow

  Data deletion           Privacy and compliance  Document deletion
  incomplete              risk                    cascade, storage
                                                  cleanup, retention
                                                  policy tests

  Dependency              Operational/security    Pin dependencies,
  vulnerabilities         risk                    update regularly, scan
                                                  and patch

  Unclear data-sharing    Loss of trust           Clear privacy notice
  practices                                       and minimal data
                                                  sharing with providers
  -----------------------------------------------------------------------
