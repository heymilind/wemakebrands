'use server'
 
import { Resend } from 'resend'

const resend = new Resend(process.env.RESEND_API_KEY)

export async function subscribeToList(formData: FormData) {
  const email = formData.get('email') as string

  try {
    await resend.emails.send({
      from: 'onboarding@resend.dev',
      to: 'milindboro004@gmail.com',
      subject: 'New Subscription from Landing Page',
      html: `New subscriber: ${email}`
    })

    return { success: true, message: 'Thanks for subscribing!' }
  } catch (error) {
    return { success: false, message: 'Something went wrong. Please try again.' }
  }
}
