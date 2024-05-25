# React Application with React-Bootstrap Form

### Check it
[https://dev-arindam-roy.github.io/react-bootstrap-form-fields-registration/](https://dev-arindam-roy.github.io/react-bootstrap-form-fields-registration/)

```js
import React, { useState } from "react";
import { FaSignInAlt, FaList } from "react-icons/fa";
import Container from "react-bootstrap/Container";
import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";
import Form from "react-bootstrap/Form";
import Button from "react-bootstrap/Button";
import Card from "react-bootstrap/Card";
import Table from 'react-bootstrap/Table';

const userObj = {
  "first_name": "",
  "last_name": "",
  "email": "",
  "password": ""
}

const App = () => {

  const [user, setUser] = useState(userObj);
  const [confirmPassword, setConfirmPassword] = useState("");
  const [isPasswordConfirmed, setIsPasswordConfirmed] = useState(true);
  const [userList, setUserList] = useState([]);

  const confirmPasswordHandler = () => {
    if (confirmPassword === user.password) {
      setIsPasswordConfirmed(true);
    } else {
      setIsPasswordConfirmed(false);
    }
    console.log(isPasswordConfirmed);
  }

  const formSubmitHandler = (e) => {
    e.preventDefault();
    console.log(isPasswordConfirmed);
    if (isPasswordConfirmed) {
      setUserList([...userList, user]);
      formReset();
    }
  };

  const formResetHandler = () => {
    formReset();
  }

  const formReset = () => {
    let _userObj = {
      "first_name": "",
      "last_name": "",
      "email": "",
      "password": ""
    }
    setUser(_userObj);
    setConfirmPassword("");
  }

  const resetUserListHandler = () => {
    setUserList([]);
    formReset();
  }

  return (
    <>
      <Container fluid="md">
        <Row className="mt-3">
          <Col md={4} xs={12}>
            <Form onSubmit={formSubmitHandler}>
              <Card>
                <Card.Header>
                  <h3 className="mb-3">
                    <FaSignInAlt className="text-primary" /> Registration Form!
                  </h3>
                </Card.Header>
                <Card.Body>
                  <Row className="mb-3">
                    <Col>
                      <Form.Group controlId="forFirstName">
                        <Form.Label>
                          First Name: <em>*</em>
                        </Form.Label>
                        <Form.Control
                          type="text"
                          name="first_name"
                          placeholder="First Name"
                          required
                          value={user.first_name}
                          onChange={(e) => setUser({...user, "first_name": e.target.value})}
                        />
                      </Form.Group>
                    </Col>
                    <Col>
                      <Form.Group controlId="forLastName">
                        <Form.Label>
                          Last Name: <em>*</em>
                        </Form.Label>
                        <Form.Control
                          type="text"
                          name="last_name"
                          placeholder="Last Name"
                          required
                          value={user.last_name}
                          onChange={(e) => setUser({...user, "last_name": e.target.value})}
                        />
                      </Form.Group>
                    </Col>
                  </Row>
                  <Form.Group className="mb-3" controlId="forEmailAddress">
                    <Form.Label>
                      Email Id: <em>*</em>
                    </Form.Label>
                    <Form.Control
                      type="email"
                      name="email"
                      placeholder="Email Address"
                      required
                      value={user.email}
                      onChange={(e) => setUser({...user, "email": e.target.value})}
                    />
                    <Form.Text className="text-muted">
                      We'll never share your email with anyone else.
                    </Form.Text>
                  </Form.Group>
                  <Form.Group className="mb-3" controlId="forPassword">
                    <Form.Label>
                      Password: <em>*</em>
                    </Form.Label>
                    <Form.Control
                      type="password"
                      name="password"
                      placeholder="Password"
                      required
                      value={user.password}
                      onChange={(e) => setUser({...user, "password": e.target.value})}
                    />
                  </Form.Group>
                  <Form.Group className="mb-3" controlId="forConfirmPassword">
                    <Form.Label>
                      Confirm Password: <em>*</em>
                    </Form.Label>
                    <Form.Control
                      type="password"
                      name="confirm_password"
                      placeholder="Confirm Password"
                      required
                      value={confirmPassword}
                      onBlur={confirmPasswordHandler}
                      onChange={(e) => setConfirmPassword(e.target.value)}
                    />
                    <Form.Text className={"text-muted" + ((isPasswordConfirmed) ? ' d-none' : ' d-block') }>
                      Confirm password not matched!
                    </Form.Text>
                  </Form.Group>
                </Card.Body>
                <Card.Footer>
                  <Button type="submit" variant="primary">
                    Register Me!
                  </Button>
                  <Button type="button" variant="danger" className="mx-2" onClick={formResetHandler}>
                    Reset
                  </Button>
                </Card.Footer>
              </Card>
            </Form>
          </Col>
          <Col md={8} xs={12}>
            <Card>
              <Card.Header>
                <h3><FaList /> User List - ({userList.length})</h3>
              </Card.Header>
              <Card.Body>
                <Table striped bordered hover size="sm">
                  <thead>
                    <tr>
                      <th>SL</th>
                      <th>NAME</th>
                      <th>EMAIL ID</th>
                      <th>PASSWORD</th>
                    </tr>
                  </thead>
                  <tbody>
                    {
                      userList.length > 0 && 
                        userList.map((item, index) => {
                          return (
                            <tr key={"userTr-" + index}>
                              <th>{index + 1}</th>
                              <td>{item.first_name + " " + item.last_name}</td>
                              <td>{item.email}</td>
                              <td>{item.password}</td>
                            </tr>
                          )
                        })
                    }
                    {
                      userList.length === 0 && (
                        <tr>
                          <td colSpan="4">No user found!</td>
                        </tr>
                      )
                    }
                  </tbody>
                </Table>
              </Card.Body>
              <Card.Footer style={{textAlign: 'right'}}>
                {
                  userList.length > 0 && (
                    <Button type="button" variant="danger" onClick={resetUserListHandler}>
                      Clear All
                    </Button>
                  )
                }
              </Card.Footer>
            </Card>
          </Col>
        </Row>
      </Container>
    </>
  );
};

export default App;
```