# [Formik](https://jaredpalmer.com/formik/docs/tutorial)

## :page_facing_up: 목차
* [Overview](#overview)
* [Gist](#gist)
* [Reducing boilerplate](#reducing-boilerplate)
* [Styled-Component](#styled-component)



## Overview

>Let's face it, forms are really verbose in React. To make matters worse, most form helpers do wayyyy too much magic and often have a significant performance cost associated with them. Formik is a small library that helps you with the 3 most annoying parts:

1. Getting values in and out of form state 
2. Validation and error messages
3. Handling form submission

<a href="http://www.youtube.com/watch?feature=player_embedded&v=uyLrwn8FdmM
" target="_blank"><img src="http://img.youtube.com/vi/uyLrwn8FdmM/0.jpg" width="600" height="315" /></a>

### Gist

```jsx
import React from 'react';
import { Formik } from 'formik';

const Basic = () => (
  <div>
    <h1>Anywhere in your app!</h1>
    <Formik
      initialValues={{ email: '', password: '' }}
      validate={values => {
        const errors = {};
        if (!values.email) {
          errors.email = 'Required';
        } else if (
          !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
        ) {
          errors.email = 'Invalid email address';
        }
        return errors;
      }}
      onSubmit={(values, { setSubmitting }) => {
        setTimeout(() => {
          alert(JSON.stringify(values, null, 2));
          setSubmitting(false);
        }, 400);
      }}
    >
      {({
        values,
        errors,
        touched,
        handleChange,
        handleBlur,
        handleSubmit,
        isSubmitting,
        /* and other goodies */
      }) => (
        <form onSubmit={handleSubmit}>
          <input
            type="email"
            name="email"
            onChange={handleChange}
            onBlur={handleBlur}
            value={values.email}
          />
          {errors.email && touched.email && errors.email}
          <input
            type="password"
            name="password"
            onChange={handleChange}
            onBlur={handleBlur}
            value={values.password}
          />
          {errors.password && touched.password && errors.password}
          <button type="submit" disabled={isSubmitting}>
            Submit
          </button>
        </form>
      )}
    </Formik>
  </div>
);

export default Basic;
```
[https://codesandbox.io/s/formik-validation-xyfxx](https://codesandbox.io/s/formik-validation-xyfxx)

### Reducing boilerplate
```jsx
// Render Prop
import React from 'react';
import { Formik, Form, Field, ErrorMessage } from 'formik';

const Basic = () => (
  <div>
    <h1>Any place in your app!</h1>
    <Formik
      initialValues={{ email: '', password: '' }}
      validate={values => {
        const errors = {};
        if (!values.email) {
          errors.email = 'Required';
        } else if (
          !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$/i.test(values.email)
        ) {
          errors.email = 'Invalid email address';
        }
        return errors;
      }}
      onSubmit={(values, { setSubmitting }) => {
        setTimeout(() => {
          alert(JSON.stringify(values, null, 2));
          setSubmitting(false);
        }, 400);
      }}
    >
      {({ isSubmitting }) => (
        <Form>
          <Field type="email" name="email" />
          <ErrorMessage name="email" component="div" />
          <Field type="password" name="password" />
          <ErrorMessage name="password" component="div" />
          <button type="submit" disabled={isSubmitting}>
            Submit
          </button>
        </Form>
      )}
    </Formik>
  </div>
);

export default Basic;
```

[https://codesandbox.io/s/formik-field-errormessage-t1hui](https://codesandbox.io/s/formik-field-errormessage-t1hui)


### Styled-Component

```jsx
const StyledSelect = styled.select`
  background-color: red;
`;

const StyledErrorMessage = styled.div`
  color: red;
`;

const StyledLabel = styled.label`
  background-color: green;
`;

const MySelect = ({ label, ...props }) => {
  const [field, meta] = useField(props);
  return (
    <>
      <StyledLabel htmlFor={props.id || props.name}>{label}</StyledLabel>
      <StyledSelect {...field} {...props} />
      {meta.touched && meta.error ? (
        <StyledErrorMessage>{meta.error}</StyledErrorMessage>
      ) : null}
    </>
  );
};
```

[https://codesandbox.io/s/formik-styled-component-dv1qu](https://codesandbox.io/s/formik-styled-component-dv1qu)

:memo: **참고 자료**   
[https://medium.com/hackernoon/react-form-validation-with-formik-and-yup-8b76bda62e10](https://medium.com/hackernoon/react-form-validation-with-formik-and-yup-8b76bda62e10)   
[https://medium.com/@rossbulat/formik-for-react-introduction-to-form-management-done-right-971889b40f9f](https://medium.com/@rossbulat/formik-for-react-introduction-to-form-management-done-right-971889b40f9f)   
[https://medium.com/teamsubchannel/react-formik-styled-components-add78b37971f](https://medium.com/teamsubchannel/react-formik-styled-components-add78b37971f)   
[https://www.youtube.com/watch?v=FD50LPJ6bjE](https://www.youtube.com/watch?v=FD50LPJ6bjE)   

:arrow_up: [위로 이동](#formik)
















